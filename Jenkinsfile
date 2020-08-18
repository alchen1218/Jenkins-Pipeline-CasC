pipeline {
    agent {
        label "non-fdb-test"
    }

    stages {
        stage("Build") {
            steps {
                echo "Building...."
                echo "node_name: ${env.node_name}"
                echo "node_label: ${env.node_labels}"
            }
        }
        stage("Test") {
            agent { 
                label "fdb-test" 
            }
            steps {
                echo "Testing...."
                echo "node_name: ${env.node_name}"
                echo "node_label: ${env.node_labels} | awk '{print $5}' "
            }
        }
        stage("Deploy") {
            steps {
                echo "Deploying...."
            }
        }
    }
}