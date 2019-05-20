pipeline {
       agent {
       docker {
             image "centos:7"
                          }
                 }
    stages {
        stage('Stage 1') {
            steps {
                sh 'mkdir -p deps'
                
                dir('deps') {
                script {
                def workspace = pwd()
                }
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/monorels/jenkins.git']]])
                }
                
                echo 'Hello world!' 
                echo "${workspace}"
            }
        }
    }
}
