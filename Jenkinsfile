pipeline {
    agent {
        label 'non-fdb-test'
    }

    stages {
        stage('Build') {
            steps {
                echo "node_name: ${env.node_name}"
                echo 'Building....'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing....'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}