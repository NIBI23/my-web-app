pipline {
    agnent any
    stages {
        stage ('Checkout') {
            steps {
                echo 'Checking out the code'
                https://github.com/NIBI23/my-web-app.git
            }
        }
        stage ('Build') {
            steps {
                echo 'Building the project'
                sh 'python3 -m pip install -r requirements.txt'
            }
        }
        stage ('Test') {
            steps {
                echo 'Running tests'
                sh 'python3 app.py &'
                sh 'curl http://localhost:5000'
            }
        }
        stage ('Deploy') {
            steps {
                echo 'Deploying the Appication'
                sh 'docker build -t my-web-app .'
                sh 'docker run -d -p 5000:5000 my-web-app'
            }
        }
    }
}
