pipeline {
    agent {
        label 'ssh-agent' // Replace with your agent's label
    }

     environment {
        MAVEN_HOME = '/opt/maven'  // Set this to your Maven installation path
        PATH = "$MAVEN_HOME/bin:$PATH"  // Add Maven to the PATH
    }

    stages {
        stage('Build') {
            steps {
                sshagent(credentials: ['ssh-agent']) {
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
