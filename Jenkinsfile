pipeline{
    agent any
    tools {
           
           maven 'Maven' 
    }
 
    stages{
        stage("Test"){
            steps{
                // mvn test
             
            
                sh 'mvn test'
                
            }
        }
            stage("Build"){
            steps{
                // mvn package
                sh "mvn package"
            }
        }

            stage("Deploy on Test"){
            steps{
                // deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: '3b1c58f7-77f7-4c26-a9b8-38a6cc9e26aa', path: '', url: 'http://192.168.0.101:8080')], contextPath: '/app', war: '**/*.war'
               
            }
        }
            stage("Deploy on Prod"){
                input {
                message "Should we continue?"
                ok "Yes we should"
            }
            steps{
                // deploy on container -> plugin
               deploy adapters: [tomcat9(credentialsId: '3b1c58f7-77f7-4c26-a9b8-38a6cc9e26aa', path: '', url: 'http://192.168.0.102:8080')], contextPath: '/app', war: '**/*.war'
               
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
