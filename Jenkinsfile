pipeline {

    agent any
    stages {
        stage ('Build'){
              steps {
                sh 'sudo docker build -t meta-api:latest .'
            }
        }
        stage('Deploy to ECR') {
            steps {
                script{
                        docker.withRegistry('https://177238635346.dkr.ecr.ap-south-1.amazonaws.com/meta-api', 'ecr:ap-south-1:my.aws.credential') {
                       def myImage= docker.build('meta-api')
                       myImage.push('latest')
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl set image deployment/meta-api meta-api=177238635346.dkr.ecr.ap-south-1.amazonaws.com/meta-api:latest'
                }
            }
        }
    }
}