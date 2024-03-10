pipeline {
    agent any
    environment{
        staging_server="23.111.182.242"
    }
    stages {
        stage('git repo & clean') {
            steps {
                bat "git clone https://github.com/al-zami-arafat/test-ci-cd.git"
            }
        }
        stage('install') {
            steps {
                bat "mvn install -f test-ci-cd"
            }
        }
        stage('test') {
            steps {
                bat "mvn test -f test-ci-cd"
            }
        }
        stage('package') {
            steps {
                bat "mvn package -f test-ci-cd"
            }
        }
    }
}