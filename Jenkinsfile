repo = "https://github.com/monorels/jenkins_test.git"
pipeline {
    agent {label 'worker_node'}
    parameters {
        string(name: 'USERID', defaultValue: '',
                description: 'Enter your userid')
    }
    stages {
        stage('Choice the repo revision') {
            steps {
                script {
                    dir('git-source-code') {
                        git(
                            url: ${repo},
                                branch: "master"
                        )
                        tagList = sh(returnStdout: true, script: "git for-each-ref --sort=-taggerdate --format '%(refname)' refs/tags  | awk -F '/' '{print \$3}'")
                    }
                        env.INPUT_PARAMS = input message: 'Please choice the revision', ok: 'Next',
                                        parameters: [
                                        choice(name: 'TAG', choices: tagList, description: 'Available tags')]
                }
                   dir ('git-source-code') {
                         deleteDir()
                                }
                   checkout scm: [$class: 'GitSCM', 
                                  userRemoteConfigs: [[url: ${repo} ]], 
                                  branches: [[name: "refs/tags/${env.INPUT_PARAMS}"]]], 
                                  poll: false
            }
        }
    }
}
