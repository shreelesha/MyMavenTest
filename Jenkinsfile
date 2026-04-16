pipeline {
    agent any

    tools {
        maven 'Maven'   // Make sure Maven is configured in Jenkins
        jdk 'JDK17'     // Configure JDK 17 in Jenkins
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/shreelesha/MyMavenTest.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify WAR') {
            steps {
                sh 'ls -l target'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/MavenWebApp.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                echo "Deploying WAR to Tomcat..."
                cp target/MavenWebApp.war /opt/tomcat/webapps/
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}
