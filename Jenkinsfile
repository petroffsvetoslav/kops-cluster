pipeline {
    agent any
    stages {
        stage('Setup parameters') {
            steps {
                script { 
                    properties([
                        parameters([
                            // string(
                            //     defaultValue: 's3://my-state-store', 
                            //     name: 'KOPS_STATE_STORE', 
                            //     trim: true
                            //     description: "S3 bucket that will store the state"
                            // ),
                            string(name: 'KOPS_STATE_STORE', defaultValue : 's3://my-state-store', description: "S3 bucket that will store the state"),
                            string(
                                defaultValue: 'cluster.k8s.local', 
                                name: 'CLUSTER_NAME', 
                                trim: true
                            ),
                            string(
                                defaultValue: 'vpc-12345678', 
                                name: 'VPC_ID', 
                                trim: true
                            ),
                            // string(
                            //     defaultValue: '10.0.0.0/16', 
                            //     name: 'NETWORK_CIDR', 
                            //     trim: true
                            // ),
                            string(
                                defaultValue: 'subnet-27bfkste542fdf82f,subnet-0bc9b753kwy6a535', 
                                name: 'SUBNET_IDS', 
                                trim: true
                            ),
                            string(
                                defaultValue: 'c5.large', 
                                name: 'MASTER_SIZE', 
                                trim: true
                            ),
                            string(
                                defaultValue: 'm5.large', 
                                name: 'NODE_SIZE', 
                                trim: true
                            ),
                            string(
                                defaultValue: '2', 
                                name: 'NODE_COUNT', 
                                trim: true
                            ),
                            string(
                                defaultValue: 'eu-central-1,us-east-1b', 
                                name: 'ZONES', 
                                trim: true
                            )
                        ])
                    ])
                }
            }
        }
        stage('Create cluster') {
            steps {
                sh 'kops create cluster --state $KOPS_STATE_STORE --name $CLUSTER_NAME --vpc $VPC_ID --subnets $SUBNET_IDS --master-size $MASTER_SIZE --node-size $NODE_SIZE --node-count $NODE_COUNT --zones $ZONES --dry-run -oyaml > cluster.yaml'
            }
        }
        stage('Deploy cluster') {
            steps {
                timeout(time: 5, unit: "MINUTES") {
                    input message: 'Do you want to approve the deploy?', ok: 'Yes'
                            }
                sh 'kops create -f cluster.yaml'
            }
        }
        stage('Validate cluster') {
            steps {
                sh 'kops valudate cluster --name=${CLUSTER_NAME} --state=s3://${BUCKET_NAME}'
            }
        }
    }
}
