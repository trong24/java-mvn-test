pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'Maven3.3.9') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'Maven3.3.9') {
                    sh 'mvn test'
                }
            }
        }

        stage('Front-end') {
            agent {
                docker { image 'node:7-alpine' }
            }
            steps {
                sh 'node --version'
            }
        }
        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'Maven3.3.9') {
                    sh 'mvn package'
                }
            }
        }
    }
}
