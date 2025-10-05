pipeline {
    agent {label "Jenkins-Agent"}
    environment {
        APP_NAME = "Register-App"
    }

    stages {
        stage ("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage ("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github' , url: 'https://github.com/Birjendra9580/Manifest-for-Regis-App.git'
            }
        }

        stage ("Update the Deployment Tags") {
            steps {
                sh """
                cat deployment.yaml
                sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                cat deployment.yaml
                """
            }
        }

        stage ("Push the changed deployment file to Git") {
            steps {
                sh """
                git config --global user.name "Birjendra9580"
                git config --global user.email "bshukla2236@gmail.com"
                git add deployment.yaml
                git commit -m "Updated deployment.yaml manifest"
                """
            }
        }
    }
}


