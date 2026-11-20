pipeline{
    agent any
    stages{
        stage('Git Checkout') {
            steps{
                git branch: 'main', url: 'https://github.com/wancheng-li/simple-java-maven-app.git'
                echo "Git repository successfully checked out"
            }
        }
    }
}
