pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code'
                git branch: 'main', url: 'https://github.com/NIBI23/my-web-app.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project'
                sh '''
                    sudo apt-get update
                    sudo apt-get install -y python3-pip
                    python3 -m pip install --upgrade pip
                    sudo pip3 install -r requirements.txt --break-system-packages
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                // Wait for the app to start
                sh 'python3 app.py & sleep 5'
                // Ensure the app is running by checking if the port is accessible
                sh 'curl --max-time 10 http://localhost:5000 || exit 1'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the Application'

                // Stop and remove any existing container
                sh 'docker stop my-web-app || true'
                sh 'docker rm my-web-app || true'

                // Build and run a new container
                sh 'docker build -t my-web-app .'
                sh 'docker run -d -p 5000:5000 --name my-web-app my-web-app'
            }
        }
    }
}
