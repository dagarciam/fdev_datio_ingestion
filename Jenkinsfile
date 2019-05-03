@Library("workflowlibs@master") _

pipeline {
    agent { label 'spark' }

    parameters {
            string(description: "UUAA", name: "uuaa", defaultValue: "")
            string(description: "Table", name: "table", defaultValue: "")
            choice(choices: "raw\nmaster\ncustom", description: "Phase", name: "phase")
            choice(choices: "punctual\ninc\nrep\ndiff", description: "Frequency", name: "freq")
            string(description: "Params", name: "params", defaultValue: "")
            choice(choices: "ingest\ntest", description: "Mode", name: "mode")
            choice(choices: "true\nfalse", description: "Naming convention", name: "naming")
            choice(choices: "true\nfalse", description: "Sync", name: "sync")
    }

    stages {
        stage('Checkout Global Library') {
            steps {
                script{
                    globalBootstrap {
                        libraryName   = "datio-workflowlibs"
                        libraryBranch = "feature/skynet"
                        entrypointParams = [
                            projectType         : "SKYNET_INGEST"
                        ]
                    }
                }
            }
        }
    }

    post {
        always {
            echo "We have been through the entire pipeline"
        }
        changed {
            echo "There have been some changes from the last build"
        }
        success {
            echo "Build successful"
        }
        failure {
            echo "There have been some errors"
        }
        unstable {
            echo "Unstable"
        }
        aborted {
            echo "Aborted"
        }
    }
}
