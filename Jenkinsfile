properties ([pipelineTriggers([githubPush()])])

node {
    git url: 'https://github.com/alchen1218/pipeline-jenkinsfile-test.git', branch: 'master'
}

pipeline {
    agent {
        label 'non-fdb-test'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}