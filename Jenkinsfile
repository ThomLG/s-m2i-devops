pipeline {
    agent any
    triggers{
    pollSCM('H/2 * * * *')
    }
    stages {
        stage('Build Application') { 
      steps {
        sh 'mvn clean install'
      }  
    }
    stage('Deploy CloudHub') {
      environment {
        ANYPOINT_CREDENTIALS = credentials('totopondi56')
      }
      steps {
        sh "mvn deploy -DmuleDeploy -Dworkers=1 -Dworker.type=Micro -Dcloud.env=${env.envName} -DcloudhubAppName=${env.cloudhubAppName} -Dmule.version=${env.muleVersion} -Dcloud.user=${ANYPOINT_CREDENTIALS_USR} -Dcloud.password=${ANYPOINT_CREDENTIALS_PSW}"
      }
    }   
            }
}
    
