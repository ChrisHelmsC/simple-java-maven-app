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
                    def scmVars = checkout scm
                    def commitHash = scmVars.GIT_COMMIT
                    echo "$commitHash"
		} 
            }
        }
        stage('Env') {
            steps {
                sh 'printenv'
		echo "${someVar}"
            }
        }
        stage('Email') {
            steps {
                script {
                    def mailRecipients = 'chris.helms.c@gmail.com'
                    def jobName = currentBuild.fullDisplayName
                    def body = 'Something ' + "${env.someVar}"

                    emailext body: "${body}",
                    mimeType: 'text/html',
                    subject: "Hello From Jenkins",
                    to: "${mailRecipients}",
                    replyTo: "${mailRecipients}"
                }
            }
        }
    }
}
