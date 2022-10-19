def gv

pipeline {
    agent any
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    echo "building jar"
                    sh 'mvn package'
                  
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building image..."
                    withCredentials([usernamePassword(credentialsId: 'DOCKER-HUB' , passwordVariable: 'PASS' , usernameVariable: 'USER')]) {
                        sh 'docker build -t jubreal30/appbuild:1.3 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push jubreal30/appbuild:1.3'
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
