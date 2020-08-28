pipeline {
    agent {
        label 'non-fdb-test'
    }

    stages {
        stage("Initialization"){
            environment {
                PATH = "/usr/sbin:/usr/bin:/sbin:/bin"
            }
            steps {
                echo 'Initializing....'
                echo "Running job: ${env.JOB_NAME}, build: ${env.BUILD_ID} on ${env.JENKINS_URL}"
                buildDescription "Executed @ ${env.NODE_LABELS.split()[5]}"
                echo "${env.PATH}"
                script {
                    def disk_size = sh(script: "df / --output=avail | tail -1", returnStdout: true).trim() as Integer
                    println("disk_size = ${disk_size}")
                    sh "mkdir testing"
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building....'
                    echo "NODE NAME: ${env.NODE_NAME}"
                    echo "NODE LABEL: ${env.NODE_LABELS.split()[5]}"
                    echo "${WORKSPACE}"
                    def name = "Alan"
                    echo "${name}"
                    script {
                        def disk_size = sh(script: "df / --output=avail | tail -1", returnStdout: true).trim() as Integer
                        println("disk_size = ${disk_size}")
                        sh "mkdir testing"
                }
                }
            }
        }
        stage('Test') {
            agent { 
                label 'fdb-test' 
            }
            steps {
                echo "'Testing....'"
                echo "NODE NAME: ${env.NODE_NAME}"
                echo "NODE LABEL: ${env.NODE_LABELS.split()[5]}"
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
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeded!'
            slackSend channel: '#alan-test-jenkinsfile-pipeline',
                  color: 'good',
                  message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
        }
        unstable {
            echo 'I am unstable'
            slackSend channel: '#alan-test-jenkinsfile-pipeline',
                  color: 'bad',
                  message: "The pipeline ${currentBuild.fullDisplayName} is unstable."
        }
        failure {
            echo 'I failed'
            slackSend channel: '#alan-test-jenkinsfile-pipeline',
                  color: 'bad',
                  message: "The pipeline ${currentBuild.fullDisplayName} has failed."
        }
        // changed {
        //     echo 'Things were different before...'
        //     slackSend channel: '#alan-test-jenkinsfile-pipeline',
        //           color: 'good',
        //           message: "Something in the pipeline ${currentBuild.fullDisplayName} has changed."
        // }
    }
}