pipeline{
    agent any
    triggers{

 pollSCM('H/2 * * * *')

    }
    stages{
        stage('Build Application')
        {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Deploy CloudHub'){
            environment{        
                ANYPOINT_CREDENTIALS = credentials('totopondi56')      
            }      
            steps {
                sh "mvn deploy -DmuleDeploy -Dmule.version=4.4.0 -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW} -Denv=Sandbox -Dappname=s-m2i-devops -Dbusiness=Unemployed1"
            }     
        }   
    }
}