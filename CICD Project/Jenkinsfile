pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "kpamrutha5/proectappforcicd:latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
                checkout([
                    $class: 'GitSCM',
                     branches: [[name: '*/main']], // Specify 'main' branch
                     userRemoteConfigs: [[
                     url: 'https://github.com/amruthakp5/CI-CD-project.git',
            ]]
        ])
            }
        }
        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Docker Push') {
            steps {
                sh 'docker login -u kpamrutha5 -p Online@20'
                sh 'docker push $DOCKER_IMAGE'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy stage placeholder'
            }
        }
    }
}
