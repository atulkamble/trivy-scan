pipeline {
    agent any

    stages {

        stage('Docker Build') {
            steps {
                script {
                    echo 'Building Docker image...'
                    sh 'docker build -t my-docker-image:${BUILD_ID} .'
                }
            }
        }

        stage('Docker Image List') {
            steps {
                script {
                    echo 'Listing Docker images...'
                    sh 'docker images'
                }
            }
        }

        stage('Install Trivy') {
            steps {
                script {
                    echo 'Installing Trivy...'
                    sh '''
                        curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
                        trivy --version
                    '''
                }
            }
        }

        stage('Trivy Scan') {
            steps {
                script {
                    echo 'Running Trivy vulnerability scan...'
                    sh 'trivy image --exit-code 1 --severity HIGH,CRITICAL my-docker-image:${BUILD_ID}'
                }
            }
        }
    }
}