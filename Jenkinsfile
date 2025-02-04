pipeline {
    agent {
        label 'ssh-agent' // Default agent for the pipeline
    }

    environment {
        MAVEN_HOME = '/opt/maven'  // Set this to your Maven installation path
        PATH = "$MAVEN_HOME/bin:$PATH"  // Add Maven to the PATH
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
