node {
    stage('Checkout'){
        checkout([$class: 'GitSCM', branches: [[name: '${tag}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'gitcreds', url: 'https://github.com/Skoul7/maven-simple.git']]])

    }}
