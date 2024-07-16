pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                git 'https://github.com/zininngg/JenkinsDependencyCheckTest.git'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                withCredentials([string(credentialsId: 'NVD_API_KEY', variable: 'NVD_API_KEY')]) {
                    dependencyCheck additionalArguments: '--format HTML --format XML --nvdApiKey ${NVD_API_KEY}', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                }
            }
        }
    }   
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
