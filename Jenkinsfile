pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                def attachments = [
                    [
                    text: 'I find your lack of faith disturbing!',
                    fallback: 'Hey, Vader seems to be mad at you.',
                    color: '#ff0000'
                    ]
                ]

                slackSend(channel: "#buildstatus", attachments: attachments)

                slackSend color: "good", message: "Message from Jenkins Pipeline"
                sh 'mvn -B -DskipTests clean package'
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
