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
        environment {
            DOCKER-HUB=credentials('DOCKER-HUB')
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
                        sh 'docker build -t jubreal30/appbuild:1.01 .'
                        sh 'docker tag jubreal30/appbuild:1.01 jubreal30/appbuild:1.1"
                        sh 'echo $DOCKER-HUB_PSW | docker login -u $DOCKER-HUB_USER --password-stdin'
                        sh 'docker push jubreal30/appbuild:1.1'
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
