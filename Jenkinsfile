pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sudo sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sudo sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sudo sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}