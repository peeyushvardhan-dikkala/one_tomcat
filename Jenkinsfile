pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
                stash name: 'compiled-artifacts', includes: 'target/**/*.jar'
            }
        }

        stage('Test') {// This could be any test node
            steps {
                unstash 'compiled-artifacts'
                sh 'java -jar target/myapp.jar --test'  // For Windows node; use `sh` on Linux
            }
        }

        
    }
}
