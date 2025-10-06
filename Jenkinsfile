pipeline {
    agent any
    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }
    stages {
        stage('Checkout') {
            steps {
                // write your logic here
                git branch: 'main',
                    url:'https://github.com/NivedithaPrakas/java-batch-job-example.git'
            }
        }
        stage('Build') {
            // write your logic here
            steps{
                bat 'mvn clean install -DskipTests'
            }
        }
        stage('Run Application') {
            // write your logic here
            steps{
            bat 'mvn exec:java -Dexec.mainClass="com.expertszen.BatchJobApp"'
            }
        }
        stage('Test') {
            // write your logic here
            steps{
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
    }
         post {
        failure {
            mail to: 'nivedithaprakashkp@gmail.com',
                 subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} failed.
                 Check console output at ${env.BUILD_URL}console"""
        }
        success {
            mail to: 'nivedithaprakashkp@gmail.com',
                 subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Job '${env.JOB_NAME}' succeeded. ${env.BUILD_URL}"
        }
    }
}
