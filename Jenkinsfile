def conf = {}
def env = {}

pipeline{
    agent any
    triggers{

 pollSCM('H/2 * * * *')

    }
    stages{

        stage('configuration'){
            /*Lire le fichier json config.json en utilisant jsonRead*/
            conf = readJSON file: "env/${env.BRANCH_NAME}/config.json"
            env = config.get("envConfig") 
        }
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
                sh "mvn deploy -DmuleDeploy -Dmule.version=4.4.0 -Danypoint.username=${ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${ANYPOINT_CREDENTIALS_PSW} -Denv=${env.environment} -Dappname=s-m2i-devops -Dbusiness=Unemployed1"
            }     
        }   
    }
}