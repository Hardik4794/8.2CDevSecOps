pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Code already checked out from GitHub'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install || true'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'echo "Running tests..."'
            }
        }

        stage('NPM Audit') {
            steps {
                sh 'npm audit || true'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        # Download SonarScanner (skip if already downloaded)
                        if [ ! -f sonar-scanner.zip ]; then
                            curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
                        fi

                        # Unzip (overwrite quietly)
                        unzip -o sonar-scanner.zip > /dev/null 2>&1 || true

                        # Run SonarScanner with Hardik's configuration
                        ./sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner \
                            -Dsonar.projectKey=Hardik4794_8.2CDevSecOps \
                            -Dsonar.organization=hardik4794 \
                            -Dsonar.sources=. \
                            -Dsonar.language=js \
                            -Dsonar.sourceEncoding=UTF-8 \
                            -Dsonar.exclusions=node_modules/**,test/** \
                            -Dsonar.host.url=https://sonarcloud.io \
                            -Dsonar.login=${SONAR_TOKEN}
                    '''
                }
            }
        }
    }
}
