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
                        def tagList = sh(returnStdout: true, script: "git for-each-ref --sort=-taggerdate --format '%(refname)' refs/tags  | awk -F '/' '{print \$3}'")//.split()
                        //tagList.each { nxtTag -> echo nxtTag }

                        def slurper = new JsonSlurper()
                        def json = slurper.parseText(tagList.map(java.util.Arrays.toString))
                        def tags = new ArrayList()
                            tags.addAll(json.tags)
                        return tags.join('\n')
                    }
                }

            }
        }
    }
}
