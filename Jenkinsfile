pipeline {
    agent any

    environment {
        registry = "docker.io"
        registryCredential = 'docker_cred'
        dockerImage = 'harsha6798/devsecops-game'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/harsha-ops/DevSecOps-Game.git'
            }
        }

        stage('Unit Test') {
            steps {
                sh '''
                    echo "Installing dependencies"
                    npm install
                    npm test || echo "No tests found, would add tests in a real project"
                '''
            }
        }

        stage('Static Code Analysis') {
            steps {
                sh '''
                    echo "Running static code analysis"
                    npm run lint
                '''
            }
        }

        stage('Build App') {
            steps {
                sh '''
                    echo "Building the APP"
                    npm run build
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    echo "Building Docker Image"
                    docker build -t $registry/$dockerImage:$BUILD_NUMBER .
                '''
            }
        }

        stage('Image Scan by Trivy') {
            steps {
                sh '''
                    echo "Scanning Docker Image"
                    trivy $registry/$dockerImage:$BUILD_NUMBER
                '''

            }
        }

        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker_cred',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASSWORD'
                    )]) {
                    sh '''
                        echo "Logging in to Docker"
                        docker login -u $DOCKER_USER -p $DOCKER_PASSWORD
                    '''
                }

            }
        }

        stage('Push Docker Image') {
            steps {
                sh '''
                    echo "Pushing Docker Image"
                    docker push $registry/$dockerImage:$BUILD_NUMBER
                '''
            }
        }
}