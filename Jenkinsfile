pipeline {
    agent {
        label 'AGENT-1'
    }
    stages {

        stage('Read the version')
        {
            steps{
                def packageJson = readJSON file: 'package.json'
                def appVersion = packageJson.version

                echo "application version is $appVersion"
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