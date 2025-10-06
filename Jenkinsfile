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
                echo 'Cloning the Repository...'
                git branch: 'main', url:'https://github.com/NivedithaPrakas/java-batch-job-example.git'
            }
        }
        stage('Build') {
            // write your logic here
            steps{
                echo 'Building the project using maven...'
                bat 'mvn clean install -DskipTests=true'
            }
        }
        stage('Test') {
            // write your logic here
            steps{
                echo 'Running Unit tests...'
                bat 'mvn test'
            }
        }
        stage('Run Application') {
            // write your logic here
            steps{
                echo 'Running the Java Batch job...'
                bat 'mvn exec:java -Dexec.mainClass="com.expertszen.BatchJobApp"'
            }
        }
    }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }

                success {
                    echo 'Build successful - sending success email.'
                    emailext(
                        subject: "Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body : """Successfully completed""",
                        to: 'nivedithaprakashkp@gmail.com',
                        mimeType: 'text/html'
                        )
            }
                failure {
                    mail to: 'nivedithaprakashkp@gmail.com',
                 subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} failed.
                 Check console output at ${env.BUILD_URL}console"""
        }
        
    }
}
