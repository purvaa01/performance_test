pipeline {
    agent any

    environment {
        JMETER_PATH = "/opt/apache-jmeter-5.6.3/bin/jmeter"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/yourusername/your-repo.git'
            }
        }

        stage('Run Performance Test') {
            steps {
                sh '''
                mkdir -p report
                ${JMETER_PATH} -n -t p_test.jmx -l results.jtl -e -o report
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'results.jtl, report/**', allowEmptyArchive: true
        }
    }
}
