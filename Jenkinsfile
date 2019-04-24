pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
    stages {
        stage('Test1') {
            steps {
                sh 'node --version'
            }
        }
    stage('Run AWS CLI') {

        agent {
            node {
                label 'kube_aws'
            }
        } // agent

        environment {
            AWS_DEFAULT_REGION = "${aws_region}"
        }

        steps {
            withCredentials([[
                $class: 'AmazonWebServicesCredentialsBinding',
                credentialsId: 'aws-pwolstenholme',
                accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
            ]]) {             
                container('aws') {
                    sh 'env | sort -u'
                    sh 'aws ec2 describe-instances'
                }
            } // withCredentials
        } // steps

    } // stage
    }
}
