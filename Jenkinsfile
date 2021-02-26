pipeline {
    agent none
    stages { 
        stage ('Continues Testing') {
            failFast true
            parallel {
                stage ('Unit Tests') {
                    agent {
                        docker { 
                            image 'python:3.9.2'
                            args '-u root --privileged'
                        }
                    }
                    steps {
                        sh """
                            pip install -r requirements.txt
                            make tests-unit
                        """
                    }
                }      
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
        stage ('Deploy Confirmation') {
            steps {
                    input ('Do you want to deploy')
                }
            }
        stage ('Deploy Success') {
            steps {
                echo 'System was deployed'
            }
        }
    }
}