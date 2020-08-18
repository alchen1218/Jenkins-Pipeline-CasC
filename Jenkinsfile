pipeline {
    agent {
        label 'non-fdb-test'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building....'
                echo "NODE NAME: ${env.node_name}"
                echo "NODE LABEL: ${env.node_labels.split()[5]}"
            }
        }
        stage('Test') {
            agent { 
                label 'fdb-test' 
            }
            steps {
                echo "'Testing....'"
                echo "NODE NAME: ${env.node_name}"
                echo "NODE LABEL: ${env.node_labels.split()[5]}"
            }
        }
        stage('Running in Parallel') {
            steps {
                parallel(
                    a: {
                        echo "building in parallel 1"
                    },
                    b: {
                        echo "building in parallel 2"
                    }
                )
            }
        }
    }
}