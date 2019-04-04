pipeline {
    agent none
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    label 'Master-Node'
                    image 'bibinwilson/jenkins-slave:latest'
                }
            } 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            agent {
                docker {
                    label 'Master-Node'
                    image 'maven:3-alpine'
                }
            }
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
            agent {
                docker {
                    label 'Master-Node'
                    image 'maven:3-alpine'
                }
            }
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
