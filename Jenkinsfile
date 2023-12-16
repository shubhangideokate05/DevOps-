pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage("Test"){
            steps{
                //mvn test
                sh 'mvn test'
                echo "Test"
            }
        }
        stage("Build"){
            steps{
                sh 'mvn package'
                echo "Build"
            }
        }
        stage("Deploy on Test"){
            steps{
                //deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails1', path: '', url: 'http://13.232.102.98:8080/')], contextPath: '/app', war: '**/*.war'
                echo "Deploy on test"
            }
        }
        stage("Deploy on Prod"){
            steps{
                //deploy on container -> plugin
                
                echo "Deploy on prod"
            }
        }
    }
    post{
        always{
            echo "Always"
        }
        success{
            echo "success"
        }
        failure{
            echo "Failure"   
        }
    }
}
