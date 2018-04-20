pipeline {
    agent any
    tools {
        maven 'the_maven'
        jdk 'jdk8'
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('packer_it') {
            steps {
              withCredentials([
                usernamePassword(
                  credentialsId: '245979750259',
                  passwordVariable: 'AWS_SECRET',
                  usernameVariable: 'AWS_KEY')
              ]) {
                sh 'packer build -var aws_access_key=${AWS_KEY} -var aws_secret_key=${AWS_SECRET} packer/packer.json'
              }
            }
        }
        stage('ship_it') {
            steps {
                echo 'not done yet'
            }
        }
    }
    post {
        success {
            junit 'target/surefire-reports/**/*.xml'
        }
    }
}
