pipeline {
    agent any

    stages {
        stage('w/0 docker') {
            steps {
                sh '''
                echo "outside docker"
                ls -la
                '''
            }
        }
        
        stage('with docker'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                echo "inside docker"
                ls -la
                npm --version
                '''
            }
        }
    }
    
    post{
        always {
            echo "I run every time, no matter what!"
            cleanWs()
        }
        success {
            echo "Build successful! Sending notification..."
        }
        failure {
            echo "Build failed! Checking logs..."
        }
    }
}
