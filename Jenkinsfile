someVar = 'something'

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
                echo 'This is a variable ${testVar}'
		script {
                    env.someVar = 'This has changed'
		} 
            }
        }
        stage('Env') {
            steps {
                sh 'printenv'
            }
        }
    }
}
