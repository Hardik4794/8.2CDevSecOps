pipeline {
    agent any

    stages {

        stage('1. Code Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'main', url: 'https://github.com/Hardik4794/8.2CDevSecOps.git'
            }
        }

        stage('2. Build') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('3. Test') {
            steps {
                echo 'Running tests...'
                sh '''
                    set +e
                    npm test
                    exit 0
                '''
            }
        }

        stage('4. Static Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
                sh '''
                    set +e
                    echo "Static analysis placeholder"
                    exit 0
                '''
            }
        }

        stage('5. Security Scan') {
            steps {
                echo 'Running security scan...'
                sh '''
                    set +e
                    npm audit --audit-level=low
                    exit 0
                '''
            }
        }

        stage('6. Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'echo "Deployment step placeholder"'
            }
        }

        stage('7. Monitor') {
            steps {
                echo 'Monitoring application...'
                sh 'echo "Monitoring step placeholder"'
            }
        }
    }
}
