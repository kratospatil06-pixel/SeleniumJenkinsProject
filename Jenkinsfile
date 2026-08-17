pipeline {
    agent any

    stages {

        stage('Check Python') {
            steps {
                bat 'where python'
                bat 'python --version'
                bat 'python -m pip --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
            }
        }

        stage('Run Selenium Tests') {
            steps {
                bat 'python -m pytest -v --html=report.html --self-contained-html'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'report.html',
                             allowEmptyArchive: true
        }

        success {
            echo 'Selenium tests completed successfully.'
        }

        failure {
            echo 'Selenium tests failed.'
        }
    }
}
