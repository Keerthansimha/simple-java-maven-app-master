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
                    sh 'mvn test'
            }
        }
        stage('Deliver') {
            steps {
                sshagent(credentials: ['ssh-1']) {
                    sh './jenkins/scripts/deliver.sh'
                }
            }
        }
    }
}
