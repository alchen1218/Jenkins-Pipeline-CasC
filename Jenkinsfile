pipeline {
    agent {
        label 'non-fdb-test'
    }
    environment {
        PATH = "/usr/sbin:/usr/bin:/sbin:/bin"
    }

    stages {
        stage("Initialization"){
            
            steps {
                echo 'Initializing....'
                echo "Running job: ${env.JOB_NAME}, build: ${env.BUILD_ID} on ${env.JENKINS_URL}"
                buildDescription "Executed @ ${env.NODE_LABELS.split()[5]}"
                echo "${env.PATH}"
                script {
                    sh "mkdir non-fdb-workspace"
                }
            }
        }
        stage('Build NON-FDB') {
            steps {
                echo "${env.PATH}"
                echo 'Building....'
                echo "NODE NAME: ${env.NODE_NAME}"
                echo "NODE LABEL: ${env.NODE_LABELS.split()[5]}"
                echo "${WORKSPACE}"
                script {
                    def name = "Alan"
                    echo "${name}"
                }
            }
        }
        stage('Test FDB') {
            agent { 
                label 'fdb-test' 
            }
            steps {
                echo "'Testing....'"
                echo "NODE NAME: ${env.NODE_NAME}"
                echo "NODE LABEL: ${env.NODE_LABELS.split()[5]}"
                script {
                    sh "mkdir fdb-workspace"
                }
                cleanWs()
            }
        }
        stage('Running in Parallel NON-FDB') {
            steps {
                parallel(
                    hello: {
                        echo "building in parallel 1"
                    },
                    world: {
                        echo "building in parallel 2"
                    }
                )
            }
        }
    }
    post {
        always {
            echo 'One way or another, I have finished'
            cleanWs() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
            slackSend channel: '#testing-jenkinsfile-pipeline',
                  color: 'good',
                  message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
        }
        unstable {
            echo 'I am unstable'
            slackSend channel: '#testing-jenkinsfile-pipeline',
                  color: 'bad',
                  message: "The pipeline ${currentBuild.fullDisplayName} is unstable."
        }
        failure {
            echo 'I failed'
            slackSend channel: '#testing-jenkinsfile-pipeline',
                  color: 'bad',
                  message: "The pipeline ${currentBuild.fullDisplayName} has failed."
        }
        // changed {
        //     echo 'Things were different before...'
        //     slackSend channel: '#testing-jenkinsfile-pipeline',
        //           color: 'good',
        //           message: "Something in the pipeline ${currentBuild.fullDisplayName} has changed."
        // }
    }
}