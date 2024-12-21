pipeline {
    agent {
        label 'AGENT-1'
    }
    environment {
        nexusUrl = 'nexus.daws78s-rev.online:8081'
    }
    stages {
        stage('Read the version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    env.appVersion = packageJson.version  // Use `env` to set global variables

                    echo "Application version is ${env.appVersion}"
                }
            }
        }

        stage('Install dependencies') {
            steps {
                sh """
                    npm install
                    ls -ltr
                    echo "Application version is ${env.appVersion}"
                """
            }
        }

        stage('Build') {
            steps {
                sh """
                    zip -q -r backend-${env.appVersion}.zip * -x Jenkinsfile -x backend-${env.appVersion}.zip
                    ls -ltr
                """
            }
        }

        stage('Nexus Artifact Upload') {
            steps {
                script {
                    nexusArtifactUploader(
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        nexusUrl: "${nexusUrl}",
                        groupId: 'com.expense',
                        version: "${env.appVersion}",
                        repository: "backend",
                        credentialsId: 'nexus-auth',
                        artifacts: [
                            [
                                artifactId: "backend",
                                classifier: '',
                                file: "backend-${env.appVersion}.zip",
                                type: 'zip'
                            ]
                        ]
                    )
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def params = [
                        string(name: 'appVersion', value: "${env.appVersion}")
                    ]
                    build job: "backend-deploy", parameters: params, wait: false
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
