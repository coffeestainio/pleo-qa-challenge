pipeline {
    agent none
    stages ('Testing') {
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
}