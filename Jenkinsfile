pipeline{
    agent any
    stages{
        stage('Download'){
            steps{
                git 'https://github.com/IntelliqDevops/maven.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Deployment'){
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'f848c409-cdbf-4a9b-90ba-2f3480794b66', path: '', url: 'http://172.31.3.151:8080/')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('Testing'){
            steps{
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/scriptedpipeline/testing.jar'
            }
        }
        stage('Delivery'){
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'f848c409-cdbf-4a9b-90ba-2f3480794b66', path: '', url: 'http://172.31.2.21:8080/')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
