pipeline {
    agent any
    stages {
        stage ('npm package') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        stage ('docker build') {
            steps {
                script {
                    sh 'docker build -t nodejsapp .'
                }
            }
        }
        stage ('container run') {
            steps {
                script {
                    sh 'docker run -itd --name nodejscont1 -p "8085:8080" nodejsapp'
                }
            }
        }
    }
    post {
        success {
            script {
                // Send a success notification to Slack
                    slackSend(
                    color: 'good',
                    message: "Build successful!",
                    channel: "selvasathis",
                    teamDomain: "nodejs",
                    tokenCredentialId: 'slack'
                    )
            }
        }
        failure {
            script {
                // Send a failure notification to Slack
                slackSend(
                    color: 'danger',
                    message: "Build failed!",
                    channel: "selvasathis",
                    teamDomain: "nodejs",
                    tokenCredentialId: 'slack'
                )
            }
        }
    }
}
