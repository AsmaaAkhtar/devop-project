pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Application build stage...' 
            }
        }
        stage('Test') {
            steps {
                // Remove existing files on the remote server first
                sh '''
                    gcloud compute ssh root@asma-apache-server --zone=us-central1-a -- "rm -rf /var/www/html/*"
                '''
                // Then copy new files from Jenkins workspace to the remote server
                sh '''
                    gcloud compute scp --recurse /var/lib/jenkins/workspace/devop-project_main/* root@asma-apache-server:/var/www/html --zone=us-central1-a
                '''
            }
        }
        stage('Run') {
            steps {
                echo 'Application run stage' 
            }
        }
    }
}
