pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2/root/.m2'
        }
    }

    stages {
        stage('Build'){
            steps{
                sh 'pwd'
                sh 'ls'
                sh 'mvn -B -DskipTests clean package'
                sh 'ls'
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver'){
            steps{
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}