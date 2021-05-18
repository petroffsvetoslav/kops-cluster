pipeline {
    agent any
    stages {
        stage('Setup parameters') {
            steps {
                script { 
                    properties([
                        parameters([
                            string(
                                defaultValue: 's3://my-state-store', 
                                name: 'KOPS_STATE_STORE', 
                                trim: true
                            ),
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
                            string(
                                defaultValue: '10.0.0.0/16', 
                                name: 'NETWORK_CIDR', 
                                trim: true
                            ),
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
    }   
}
