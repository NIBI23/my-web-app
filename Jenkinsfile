pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                echo 'Checking out the code'
                git branch: 'main', url: 'https://github.com/NIBI23/my-web-app.git'
            }
        }

        stage('Build') {
        echo 'Building the project'
        sh '''
            sudo apt-get update
            sudo apt-get install -y python3-pip
            python3 -m pip install --upgrade pip
            sudo pip3 install -r requirements.txt --break-system-packages
       '''
       }


        stage('Test') {
            steps {
                echo 'Running tests'
                sh 'python3 app.py & sleep 5'  // Wait for the app to start
                sh 'curl http://localhost:5000'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the Application'

                // Stop and remove any running container with the same name
                sh 'docker stop my-web-app || true'
                sh 'docker rm my-web-app || true'

                // Build and run a new container
                sh 'docker build -t my-web-app .'
                sh 'docker run -d -p 5000:5000 --name my-web-app my-web-app'
            }
        }
    }
}
