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
                sshagent(credentials: ['ssh-agent']) {  // Use ssh-agent for Build
                    sh 'mvn -B -DskipTests clean package'
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'  // Running tests without SSH agent
            }
        }
        
        stage('Deliver') {
            steps {
                sshagent(credentials: ['ssh-1']) {  // Use ssh-1 for Deliver stage
                    sh './jenkins/scripts/deliver.sh'
                }
            }
        }
    }
}
