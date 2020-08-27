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
                sh "mkdir -p $WORKSPACE/non-fdb-workplace;"
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
                sh "mkdir -p $WORKSPACE/fdb-workplace;"
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
    post {
        always {
            echo 'One way or another, I have finished'
            // deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
            // slackSend channel: '#wavefront-slackchannel-placeholder',
            //       color: 'good',
            //       message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
        }
        unstable {
            echo 'I am unstable'
            // slackSend channel: '#wavefront-slackchannel-placeholder',
            //       color: 'good',
            //       message: "The pipeline ${currentBuild.fullDisplayName} is unstable."
        }
        failure {
            echo 'I failed'
            // slackSend channel: '#wavefront-slackchannel-placeholder',
            //       color: 'good',
            //       message: "The pipeline ${currentBuild.fullDisplayName} has failed."
        }
        changed {
            echo 'Things were different before...'
            // slackSend channel: '#wavefront-slackchannel-placeholder',
            //       color: 'good',
            //       message: "Something in the pipeline ${currentBuild.fullDisplayName} has changed."
        }
    }
}