pipeline{
    agent any
    environment {
        APP_NAME = "simple-order-app"
        BUILD_VERSION = "1.0.${BUILD_NUMBER}"
        MAVEN_HOME = "/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/maven-3"
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }
    stages{
        stage('Install Maven') {
            steps {
                sh 'mvn -version'
                sh 'whoami'
                echo "Maven successfully installed"
            }
        }

        stage('Check Java Environment') {
            steps{
                echo 'Checking Java Version on Jenkins Agent'
                sh 'java -version'
            }
        }
        
        stage('Git Checkout') {
            steps{
                git branch: 'main', url: 'https://github.com/wancheng-li/simple-java-maven-app.git'
                echo "Git repository successfully checked out"
            }
        }

        stage('Run Unit Test') {
            steps{
                echo 'Running Junit test cases'
                sh 'mvn test'
            }
        }
        
        stage('Build with Maven') {
            steps{
                sh 'mvn clean package'
                echo "Maven build completed successfully"
            }
        }

        stage('Verify Artifact') {
            steps{
                echo 'Listing generated build artifacts'
                sh 'ls -l target/'
            }
        }
        
    }

    post {
        success {
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            echo "Build artifacts archived successfully"
        }
        failure {
            echo "Build failed. Please check the logs for details."
        }
    }
}
