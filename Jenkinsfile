pipeline {
    agent {label 'slave'}
    stages {
        stage('preparation'){
            steps {
                git 'https://github.com/METoubar/Booster_CI_CD_Project.git'
            }
        }

        stage('build Image'){
            steps {
                sh 'docker build -f django_app . -t mtoubar/jenkins_node:v1.0'
            }
        }

        stage('push Image'){
            steps {
                withCredentials([usernamePassword(credentialsId:"docker",usernameVariable:"USERNAME",passwordVariable:"PASSWORD")]) {
                    sh 'docker login --username $USERNAME --password $PASSWORD'
                    sh 'docker push mtoubar/jenkins_node:v1.0'
                }
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker run -d -p 3000:3000 mtoubar/jenkins_node:v1.0'
            }
        }
    }
}
