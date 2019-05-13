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
		echo "${someVar}"
            }
        }
        stage('Email') {
    steps {
        script {
            def mailRecipients = 'dc@xwave.de'
            def jobName = currentBuild.fullDisplayName
            emailext body: '''${SCRIPT, template="groovy-html.template"}''',
            mimeType: 'text/html',
            subject: "[Jenkins] ${jobName}",
            to: "${mailRecipients}",
            replyTo: "${mailRecipients}",
            recipientProviders: [[$class: 'CulpritsRecipientProvider']]
        }
    }
}
    }
}
