pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM (automatically handled if using "Pipeline script from SCM")
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
                // Stash the WAR file after build
                stash name: 'war-artifact', includes: 'target/*.war'
            }
        }

        stage('Test') {
            steps {
                unstash 'war-artifact'
                // Example of using the WAR file: move, verify, or deploy
                sh 'ls -lh target/'    // List to confirm the .war file is there
                // You might want to run integration tests here or deploy to a test server
            }
        }

        stage('Deploy') {
            steps {
                unstash 'war-artifact'
                // Example deployment step
                sh '''    
                    echo "Deploying WAR..."
                    cp target/myweb-*.war /opt/tomcat/apache-tomcat-9.0.104/webapps/
                    # Or use curl/scp to upload it to a server
                '''
            }
        }
    }
}
