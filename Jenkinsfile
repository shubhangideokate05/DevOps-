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
                sh 'mvn package'
            }
        }
        stage("Deploy on Mock Server"){
            steps{
                //deploy on container -> plugin
                echo "Deploying on mock server........"
                deploy adapters: [tomcat9(credentialsId: 'Snehal', path: '', url: 'http://13.126.144.165:8080')], contextPath: '/myDeclarativePipeline', war: '**/*.war'
                
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
                deploy adapters: [tomcat9(credentialsId: 'Snehal', path: '', url: 'http://65.0.98.14:8080')], contextPath: '/myDeclarativePipeline', war: '**/*.war'
            
                
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
