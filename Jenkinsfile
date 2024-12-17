pipeline {
    agent {
        label 'AGENT-1'
    }
    stages {
        stage('Build') {
            steps {
                echo 'This is Build'
            }
        }
        stage('Test') {
            steps {
              sh  """
                ls -ltr
               """
            }
        }
        stage('Deploy') {
            steps {
                echo 'This is Deploy stage'
            }
        }
    }
}