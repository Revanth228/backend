pipeline {
    agent {
        label 'AGENT-1'
    }
    environment{
        def appVersion = ''   //variable declaration
        nexusUrl: 'nexus.daws78s-rev.online:8081'

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
        stage('Build') {
            steps {
                sh  """
                zip -q -r backend-${appVersion}.zip * -x jenkinsfile -x backend-${appVersion}.zip
                ls -ltr
               """
            }
        }

         stage('Nexus Artifact Upload') {
            steps {
                script{
                    nexusArtifactUploader(
        nexusVersion: 'nexus3',
        nexusUrl: "${nexusUrl}"
        protocol: 'http',
        
        groupId: 'com.expense',
        version: "${appVersion}",
        repository: "backend",
        credentialsId: 'nexus-auth',
        artifacts: [
            [artifactId: "backend",
             classifier: '',
             file: "backend-"+"${appVersion}"  + '.zip',
             type: 'zip']
        ]
     )
                }
            }
        }
        
    }
    post {
    always {
       
          deleteDir()
    }
}


}