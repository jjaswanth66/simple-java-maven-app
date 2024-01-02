pipeline {
    agent {
        docker {
            image 'maven:latest'
            args '-v /opt/jenkins/simple-java-maven-app'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install -Dmaven.repo.local=/opt/jenkins'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
