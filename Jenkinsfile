pipeline {

        agent {
            node {
                label 'workstation'
            }
        }

        options {
            ansiColor('xterm')
        }

        parameters {

              string(name: 'component', defaultValue: '', description: 'Provide Component Name')

              string(name: 'app_version', defaultValue: '', description: 'Provide APP Version')

        }

        stages {

            stage('Clone APP Repo') {
                steps {
                    dir('APP') {
                        git branch: 'main', url: 'https://github.com/SurendraBabuC01/${component}.git'
                    }
                        dir('HELM') {
                        git branch: 'main', url: 'https://github.com/SurendraBabuC01/roboshop-helm.git'
                    }
                }
            }

            stage('Helm Deploy') {
                steps {
                    dir('HELM') {
                         sh 'helm upgrade -i ${component} . -f ../APP/values.yaml --set app_version=${app_version}'
                    }
                }
            }
        }

        post {
           always {
                 cleanWs()
           }
        }
}