node {
    stage('Checkout'){
        checkout([$class: 'GitSCM', branches: [[name: '${Tag}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'gitcreds', url: 'https://github.com/Skoul7/maven-simple.git']]])

    }}
