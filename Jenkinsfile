pipeline {
    agent any

    environment {
        APP_NAME = "spring-boot-hello-world"
        REPO_URL = "${params.repoUrl}"
        BRANCH = "${params.branch}"
        OWNER = "${params.owner}"
        JAR_FILE = "target/spring-boot-hello-world-1.0.2-SNAPSHOT.jar"
    }

    stages {
        stage('Fetch Code') {
            steps {
                script {
                    // Clone the repository
                    checkout([$class: 'GitSCM', branches: [[name: "${BRANCH}"]], userRemoteConfigs: [[url: "${REPO_URL}"]]])
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the Spring Boot application
                    sh "mvn clean install"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy the Spring Boot application
                    sh "java -jar ${JAR_FILE}"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}
