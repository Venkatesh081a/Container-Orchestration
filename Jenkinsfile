pipeline {
    agent any
    environment {
        FRONTEND_IMAGE = "venky081/react-app:v1"
        BACKEND_IMAGE = "venky081/node-app:v1"
        HELM_CHART_DIR = "./Helm Chart"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Venkatesh081a/Container-Orchestration.git'
            }
        }

        stage('Build Frontend') {
            steps {
               sh 'docker build -t $FRONTEND_IMAGE ./frontend'
            }
        }

         stage('Build Backend') {
            steps {
               sh 'docker build -t $BACKEND_IMAGE ./backend'
            }
        }

        stage('Push Frontend Image') {
            steps {
               sh 'docker push $FRONTEND_IMAGE'
            }
        }

        stage('Push Backend Image') {
            steps {
               sh 'docker push $BACKEND_IMAGE'
            }
        }

        stage('Deploy with Helm chart') {
            steps {
                sh """
                    helm upgrade --install mern-app $HELM_CHART_DIR/
                    --set frontend.image = $FRONTEND_IMAGE
                    --set backend.image = $BACKEND_IMAGE
                    --set backend.mongoUri = "mongodb://bW9uZ29kYjovL21vbmdvZGItc2VydmljZS5kYXRhYmFzZS5zdmMuY2x1c3Rlci5sb2NhbDoyNzAxNy90bW1lcm4="
                """
            }
        }
    }

    post{
        always{
            cleanWs()
        }
    }
}
