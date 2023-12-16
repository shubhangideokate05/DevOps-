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
                //mvn package
                sh 'mvn package'
                echo "Build"
            }
        }
        stage("Deploy on Test"){
            steps{
                //deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'newID2', path: '', url: 'http://65.1.91.110:8080')], contextPath: '/myApp', war: '**/*.war'
                echo "Deploy test"
            }
        }
        stage("Deploy on Prod"){
            steps{
                //deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'newID2', path: '', url: 'http://13.233.142.124:8080')], contextPath: '/myApp', war: '**/*.war'
                echo "Deploy Prod"
                
            }
        }
    }
    post{
        always{
            echo "Always"

        }
        success{
                echo "Success"
        }
        failure{
                echo "Failure"
        }
    }
}
