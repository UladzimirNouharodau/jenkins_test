import groovy.json.JsonSlurper

pipeline {
    agent {label 'worker_node'}
    parameters {
        string(name: 'USERID', defaultValue: '',
                description: 'Enter your userid')
    }
    stages {
        stage('Login1') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/master']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/monorels/jenkins_test.git']]])
                echo "${workspace}"
            }
        }
        stage('Login2') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/master']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/monorels/jenkins.git']]])
                echo "${workspace}"
            }
        }
        stage('Login3') {
            steps {
                script {
                    dir('git-source-code') {
                        git(
                                url: "https://github.com/monorels/jenkins_test.git",
                                branch: "master"
                        )
                        tagList = sh(returnStdout: true, script: "git for-each-ref --sort=-taggerdate --format '%(refname)' refs/tags  | awk -F '/' '{print \$3}'")//.split()
                    }
                        def INPUT_PARAMS = input message: 'Please Provide Parameters', ok: 'Next',
                                        parameters: [
                                        choice(name: 'IMAGE_TAG', choices: tagList, description: 'Available tags')]
                }
            }
        }
    }
}
