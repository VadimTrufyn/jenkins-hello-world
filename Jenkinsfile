pipeline {
    agent any
    tools {
        maven 'Maven3.9.6'
    }
    stages {
        stage("init") {
            steps {
                script {
                    echo "init"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    echo "building jar"
                    sh "mvn package"
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building image"
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker build -t truefunnny/test-repo:jmv-1 ."
                        sh 'docker push truefunnny/test-repo:jmv-1'
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                }
            }
        }
    }   
}
