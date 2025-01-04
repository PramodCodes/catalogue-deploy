// Jenkinsfile (Declarative Pipeline) 
pipeline{
    agent {
        // run on the AGENT-1 node
        node {
            label 'AGENT-1'
        }
    }
    // parameters section, this section is used to define the parameters that can be used in the pipeline
    // define the environment variables canbe accesed globally ,the following are additional to existing environment variables
    // we use ansiColor plugin to print the logs in color
    options {
        ansiColor('xterm')
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
    // we need to get version from the application for this we use pipeline, for this we will use pipeline utilities plugin
    // this can be used across pipeline
    // environment {
    //     packageVersion = ''
    //     nexusURL = '172.31.92.207:8081'
    // }
    
    parameters {
        string(name: 'version', defaultValue: '1.0.0', description: 'what is the artifact version?')
        string(name: 'environment', defaultValue: 'dev', description: 'what is the Environment?')

    }
    
    //build stages
    stages {
        stage('Print Version') {
            steps {
                sh """
                    echo "version is ${params.version}"
                """
            }
        }
    }

    // post section
    post {
        always {
            echo 'This will always run irrespective of status of the pipeline'
            // you need to delete workspace after the build because we are using the same workspace for all the builds
            deleteDir()
        }
        failure {
            echo 'This will run only if the pipeline is failed, We use thsi for alerting the team' 
        }
        success {
            echo 'This will run only if the pipeline is successful'
        }
    }
}
