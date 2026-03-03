pipeline {
    agent {
        label "jenkins-agent-01"
    }
    tools {
        maven "maven-3-6-3"
        jdk "jdk-11"
    }
    environment {
        DOCKER_USERNAME = credentials("docker-username")
        DOCKER_PASSWORD = credentials("docker-password")
    }
    stages {
        stage("Build Application") {
            steps {
                sh "mvn package install -DskipTests"
            }
        }
        stage("Test Application") {
            steps {
                sh "mvn test"
            }
        }
        stage("Build Docker Image") {
            steps {
                sh "docker build -t meno0123/java-project:v${BUILD_NUMBER} ."
            }
        }
        stage("Push Image") {
            steps {
                sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                sh "docker push meno0123/java-project:v${BUILD_NUMBER}"
            }
        }
    }
}