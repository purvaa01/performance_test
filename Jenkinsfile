pipeline {
    agent any

    environment {
        JMETER_PATH = "/opt/apache-jmeter-5.6.3/bin/jmeter"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/purvaa01/performance_test.git'
            }
        }

       stage('Performance Testing') {
           steps {
               sh '''
               rm -rf report
               rm -f results.jtl

               mkdir report

               /opt/apache-jmeter-5.6.3/bin/jmeter \
               -n -t p_test.jmx \
               -l results.jtl \
               -e -o report
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
