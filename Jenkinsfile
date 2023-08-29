pipeline {
    agent {label 'slave'}


    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/pawanappikatla/git-actions.git'
                sh "ls -ltr"
            }
        }
        stage('Setup') {
            steps {
                sh "pip install -r requirements.txt"
            }
        }
        stage('Test') {
            steps {
                sh "pytest test.py"
            }
        }
        stage('Build Docker Image')
        {
            steps
            {
                sh 'sudo -S docker build -t pawanappikatla/git-actions.git.'
                echo "Docker image build successfully"
                sh "docker images"
            }
        }
        stage('Push Docker Image')
        {
            steps
            {
                sh 'sudo -S docker push pawanappikatla/git-actions.git'
                echo "Docker image push successfully"
            }
        }
        stage('Deploy new Docker Image')
        {
            steps
            {   sh 'sudo -S docker rm -f flaskapp'
                sh 'sudo -S docker rmi pawan/jenkins-flask'
                sh 'sudo -S docker run --name flaskapp -itd -p 5001:5001 pawan/jenkins-flask'
                echo "Docker image push successfully"
            }
        }
    }
}
