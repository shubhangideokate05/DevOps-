pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage("Test"){
            steps{
                //mvn test
                echo "Testing......."
                bat 'mvn test'
            }
        }
        stage("Build"){
            steps{
                //mvn package
                echo "Building....."
                bat 'mvn package'
            }
        }
        stage("Deploy on Mock Server"){
            steps{
                //deploy on container -> plugin
                echo "Deploying on mock server........"
                deploy adapters: [tomcat9(credentialsId: 'Tomcat Credentials', path: '', url: 'http://localhost:8081/')], contextPath: '/Test', war: '**/*.war'
                
            }
        }
        stage("Deploy on Production Server"){ 
            input{
                message "Should we continue?"
                ok "Yes we should"
            }
            
            steps{
                echo "Deploying on Production Server......."
                //deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'Tomcat Credentials', path: '', url: 'http://localhost:8081/')], contextPath: '/Production', war: '**/*.war'
            
                
            }
        }
    }
    post{
        always{
            echo "_______________Always_______________"

        }
        success{
                echo "________________Success___________________"
        }
        failure{
                echo "______________Failure________________"
        }
    }
}
