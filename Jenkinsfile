pipeline {
    agent any
    tools{
        maven 'Maven3.9.6'
    } 
    stages {
        stage('build') {
            steps {
                scripts{
                    echo 'start build'
                }
            }
        }
        stage('build image') {
            steps {
                scripts{
                    echo 'start build image'
                }
            }
        }
    }
}