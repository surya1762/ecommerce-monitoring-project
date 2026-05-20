pipeline {
    agent any

    stages {

        stage('Pull Latest Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/surya1762/ecommerce-monitoring-project.git'
            }
        }

        stage('Pull Files From S3') {
            steps {
                sh '''
                aws s3 sync s3://ecommerce-monitoring-project-s3/site1 ./nginx-site
                aws s3 sync s3://ecommerce-monitoring-project-s3/site2 ./apache-site
                '''
            }
        }

        stage('Docker Compose Build') {
            steps {
                sh 'docker compose down'
                sh 'docker compose up -d --build'
            }
        }

        stage('Verify Containers') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
