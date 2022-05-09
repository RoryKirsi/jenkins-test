pipeline {
    agent any
    stages {
        stage('Prepare') {
            steps {
                sh 'git submodule update --init --recursive'
            }
        }
        stage("Docker login"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'myregistry-login', passwordVariable: 'DOCKER_REGISTRY_PWD', usernameVariable: 'DOCKER_REGISTRY_USER')]) {
                sh "docker login -u ${DOCKER_REGISTRY_USER} -p ${DOCKER_REGISTRY_PWD}"
                }
            }
        }
        stage('Build') {
            //when { expression { (params.TEST_ONLY!="true") } }
            steps {
                sh 'docker run --rm -t -v $(pwd):/src klakegg/hugo:0.93.2'
          }
        }
    }
}

