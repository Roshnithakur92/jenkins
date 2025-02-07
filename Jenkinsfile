pipeline {
    agent any
	
	environment {
        GOOGLE_CREDENTIALS = credentials('account')
}

    stages {
	     stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Roshnithakur92/project-demo.git'
            }
        }
             stage('Authenticate with Google Cloud') {
            steps {
                script {
                         // Authenticate with Google Cloud using the service account credentials
                    sh 'gcloud auth activate-service-account --key-file=${GOOGLE_CREDENTIALS}'
		    sh 'gcloud auth configure-docker us-central1-docker.pkg.dev'
	            sh 'gcloud config set project halogen-order-447007-t3'
		        }
            }
        }
		
		stage('Build Docker Image') {
            steps {
                sh 'docker build -t "us-central1-docker.pkg.dev/halogen-order-447007-t3/terraform/jenkinsimage:latest" .'
            }
        }
        
        stage('Push to Artifact Registry') {
            steps {
		         sh 'docker push "us-central1-docker.pkg.dev/halogen-order-447007-t3/terraform/jenkinsimage:latest"'
             }
         }
     }
   }
