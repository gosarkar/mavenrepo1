pipeline{
    //agent{
        //label "node"
    //}
    agent any
    
    environment{
        groovyHome = tool name: 'Groovy', type: 'hudson.plugins.groovy.GroovyInstallation'
    }

    stages{
        stage("Check-out pipeline script"){
            steps{
                dir('pipelinescript'){
                    script{
                       currentBuild.displayName = "#${BUILD_NUMBER} ${branchName}"
                    }
                    echo "======== executing check-out pipeline script repo ========"
                    checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: "*/${branchName}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/gosarkar/pipelinescript.git']]]
                }
                bat groovyHome+'/bin/groovy pipelinescript/script/script1 arg1'
                
                
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
