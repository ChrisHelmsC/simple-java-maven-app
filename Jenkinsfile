pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    environment {
        testVar = 'A value'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'echo env.testVar' 
            }
        }
        stage('Env') {
            steps {
                sh 'printenv'
            }
        }
    }
}
