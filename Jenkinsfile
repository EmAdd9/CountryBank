pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/EmAdd9/CountryBank.git'
            }
        }
        stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'owasp'
                     dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Trivy') {
            steps {
                 sh "trivy fs ."
            }
        }
        stage('Buld and Deploy') {
            steps {
                 sh "docker-compose up -d"
            }
        }
    }
}
