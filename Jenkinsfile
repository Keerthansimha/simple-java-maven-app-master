pipeline {
    agent {
        label 'ssh-agent' // Replace with your agent's label
    }
    stages {
        stage('Build') {
            steps {
                sshagent(credentials: ['your-ssh-credentials-id']) {
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        stage('Test') {
            steps {
                sshagent(credentials: ['your-ssh-credentials-id']) {
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sshagent(credentials: ['your-ssh-credentials-id']) {
                    sh './jenkins/scripts/deliver.sh'
                }
            }
        }
    }
}
