pipeline {
    agent {
        label 'AGENT-1'
    }
    environment{
        def appVersion = ''   //variable declaration
    }
    stages {

        stage('Read the version')
        {
            steps{
                script{
                def packageJson = readJSON file: 'package.json'
                appVersion = packageJson.version

                echo "application version is $appVersion"
                }
            }
        }
        stage('Install dependencies') {
            steps {
                sh  """
                npm install
                ls -ltr
                echo "application version is $appVersion"

               """
            }
        }
        
        
    }
}