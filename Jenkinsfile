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

        }

        stages {

            stage('Clone APP Repo') {
                steps {
                    dir('APP') {
                        git branch: 'main', url: 'https://github.com/SurendraBabuC01/${component}.git'
                    }
                }
            }

            stage('Helm Deploy') {
                steps {
                    sh 'helm upgrade -i ${component} . -f APP/values.yml'
                }
            }
        }