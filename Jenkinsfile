pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building website...'
                sh '''
                    rm -rf dist
                    mkdir -p dist
                    cp index.html dist/
                    echo "Build completed."
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing website...'
                sh '''
                    test -f dist/index.html
                    grep -qi "<html" dist/index.html
                    grep -qi "<title>" dist/index.html
                    grep -qi "</html" dist/index.html
                    echo "All tests passed."
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website...'
                sh '''
                    cp dist/index.html /var/www/jenkins-demo/
                    chmod 755 /var/www/jenkins-demo/index.html
                    echo "Deployment completed successfully."
                '''
            }
        }

        stage('Verify') {
            steps {
                echo 'Verifying deployment...'
                sh '''
                    sleep 2
                    curl --fail --silent http://localhost:8081 > /dev/null
                    echo "Deployment verified successfully."
                '''
            }
        }
    }
}
