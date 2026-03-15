pipeline {
    agent any

    stages {
        stage('Build'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                ls -la
                npm --version
                node --version
                npm ci
                npm run build
                ls -la
                '''
            }
        }
        stage('test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                    sh '''
                    echo "runnning tests"
                    [ -f build/index.html ] && echo "File exists."
                    npm test
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
