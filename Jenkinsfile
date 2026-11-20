pipeline{
    agent any
    stages{
        stage('Install Maven') {
            steps {
                sh '/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/maven-3/bin/mvn -version'
                echo "Maven successfully installed"
            }
        }

        stage('Git Checkout') {
            steps{
                git branch: 'main', url: 'https://github.com/wancheng-li/simple-java-maven-app.git'
                echo "Git repository successfully checked out"
            }
        }

        stage('Build with Maven') {
            steps{
                sh '/var/jenkins_home/tools/hudson.tasks.Maven_MavenInstallation/maven-3/bin/mvn clean package'
                echo "Maven build completed successfully"
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
