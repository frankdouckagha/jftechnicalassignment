pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK 17'
        jfrog 'jfrog-cli'   
    }
    environment {
        IMAGE_NAME = "spring-petclinic"
        IMAGE_TAG = "${BUILD_ID}"
        DOCKER_REPO = "jftest2.jfrog.io/jftest2-docker"
        DOCKER_USERNAME = credentials('docker-username')
        DOCKER_PASSWORD = credentials('docker-password')
    }

    stages {
        stage('Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/frank241/pet-clinic.git'
            }
        }

        stage('Compile Code') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package as Jar') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("${DOCKER_REPO}/${IMAGE_NAME}:${IMAGE_TAG}", '.')
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh '''
                echo "$DOCKER_PASSWORD" | docker login jftest2.jfrog.io -u "$DOCKER_USERNAME" --password-stdin
                docker push ${DOCKER_REPO}/${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }


    }
    
    post {
        always {
            echo 'Pipeline complete.'
        }
        success {
            echo 'Pipeline executed successfully.'
        }
        failure {
            echo 'Pileline failed.'
        }
    }
}
