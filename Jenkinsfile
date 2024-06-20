pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mv -B -DskipTests clean package'
            }
        }
    }
}
