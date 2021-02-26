pipeline {
    agent none
    stages {       
        stage ('E2E Tests') {
            agent {
                docker { 
                    image 'echowuhao/pywright'
                    args '-u root --privileged'
                }
            }
            steps {
                sh """
                    pip install -r requirements.txt
                    make pw-dependencies
                    make run &
                    sleep 3
                    make tests-e2e
                """
            }
        }
    }
}