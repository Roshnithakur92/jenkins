pipeline {
    agent any

stages {
	     stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Roshnithakur92/jenkins.git'
            }
        }
             stage('Authenticate with Google Cloud') {
            steps {
                script {
                         // Authenticate with Google Cloud using the service account credentials
			withCredentials([[$class: 'GoogleServiceAccountCredentials', credentialsId: 'google-service-account']])
			withCredentials([[$class: 'GoogleServiceAccountCredentials', credentialsId: 'google-service-account']])
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
