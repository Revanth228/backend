pipeline {
    agent {
        label 'AGENT-1'
    }
    stages {
        stage('Install dependencies') {
            steps {
                sh  """
                npm install
               """
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