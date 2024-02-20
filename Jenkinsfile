pipeline {
    agent any

    tools {
        nodejs 'nodejs-21'
    }


    stages {
        stage('checkout') {
            steps {
               git branch: 'main', changelog: false, poll: false, url: 'https://github.com/4RSIM3R/node-api'
            }
        }

        // stage('install') {
        //     steps {
        //        sh "npm install"
        //     }
        // }

        // stage('owasp_check') {
        //     steps {
        //         dependencyCheck additionalArguments: '--scan ./ --format HTML', odcInstallation: 'depesndency-check-9'
        //         dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        //     }
        // }

         stage('build') {
            steps {

                script {
                    withDockerRegistry(credentialsId: 'ilzam-docker', toolName: 'docker') {
                        sh "docker build -t node-jenkins ."
                        sh "docker tag node-jenkins ilzam/node-jenkins:latest"
                        sh "docker push ilzam/node-jenkins:latest"
                    }
                }

            }
        }
        

    }
}
