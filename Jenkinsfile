pipeline {
    agent {label 'worker_node'}
    parameters {
        string(name: 'USERID', defaultValue: '',
                description: 'Enter your userid')
    }
    stages {
        stage('Login') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/master']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/monorels/jenkins2.git']]])
                echo "${workspace}"
            }
        }
    }
}
