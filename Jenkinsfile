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
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'c343837b-ee02-4b32-8485-e557826c5fec', path: '', url: 'http://172.31.10.83:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('Testing'){
            steps{
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/scriptedpipeline@2/testing.jar'
            }
        }
        stage('Delivery'){
            steps{
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '1321c749-af3c-45be-9689-b9223f309263', path: '', url: 'http://172.31.10.247:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
