pipeline {
    agent any 
    stages {
        stage('Stage 1') {
            steps {
                sh 'mkdir -p themes deps'
                dir('deps') {
                checkout resolveScm(source: git('https://github.com/monorels/jenkins.git'), targets: [BRANCH_NAME, 'master'])
                }
                #checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/monorels/jenkins.git']]])
                echo 'Hello world!' 
            }
        }
    }
}
