pipeline{
 
    agent any
 
    parameters{
        string(name:'tomcat-stage',defaultValue:'C:/dev/jenk_serveurs/apache-tomcat-8.5.53/webapps') 
    }
 
    triggers{
        pollSCM('* * * * *')
    }
 
    stages{
 
        stage('Build'){
            
            steps{
                bat 'mvn clean package'
            }
 
            post{
                success{
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
 
        stage('Deploy'){
 
            parallel{
 
                stage('Stage Deployment'){
                    
                    steps{
 
                        echo 'Triggering Stage Deployment'
                        bat 'copy ${**/target/*.war} ${params.tomcat_prod}'
                    }
                    
                }

            }
        }
    }
}
