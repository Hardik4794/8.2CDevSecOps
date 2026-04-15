pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = tool 'SonarScanner'
    }

    stages {

        stage('1. Code Checkout') {
            steps {
                git 'https://github.com/Hardik4794/8.2CDevSecOps.git'
            }
        }

        stage('2. Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('3. SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                    $SONAR_SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.projectKey=Hardik4794_8.2CDevSecOps \
                    -Dsonar.organization=hardik4794 \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }

        stage('4. Quality Gate') {
            steps {
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: false
                }
            }
        }

        stage('5. npm Audit') {
            steps {
                sh 'npm audit --audit-level=high || true'
            }
        }

        stage('6. Deploy') {
            steps {
                sh 'echo Deployment step'
            }
        }
    }
}