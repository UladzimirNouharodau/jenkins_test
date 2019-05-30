//Get variable with repo from Jenkins parameters
env.REPO = "${GIT_URL_NAME}"

pipeline {
    agent {label 'worker_node'}
    stages {
        stage('Choice the repo revision') {
            steps {
                script {
                    dir('git-source-code') {
                        git(
                            url: env.REPO,
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
                                  userRemoteConfigs: [[url: "${env.REPO}" ]], 
                                  branches: [[name: "refs/tags/${env.INPUT_PARAMS}"]]], 
                                  poll: false
                
                   checkout scm: [$class: 'GitSCM', 
                                  userRemoteConfigs: [[url: "https://github.com/monorels/jenkins_test.git" ]], 
                                  branches: [[name: '*/master']]], 
                                  poll: false
            }
        }
    }
}
