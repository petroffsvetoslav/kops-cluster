pipeline {
    agent any
    stages {
        stage('Define parameters')
            steps {
                properties([parameters([string(defaultValue: 's3://my-state-store', description: 'S3 bucker URL', name: 'KOPS_STATE_STORE'), string(defaultValue: 'eu-central-1', description: 'Select region', name: 'AWS_REGION'), string(defaultValue: 'c5.large', description: 'Instance type for the master', name: 'MASTER_SIZE'), string(defaultValue: 'm5.large', description: 'Instance type for the nodes', name: 'NODE_SIZE'), string(defaultValue: '3', description: 'Number on nodes', name: 'NODE_COUNT'), string(defaultValue: 'eu-central-1,us-east-1b', description: 'Select AZs', name: 'ZONES'), string(defaultValue: 'cluster.k8s.local', description: 'The cluster name', name: 'CLUSTER_NAME'), string(defaultValue: 'vpc-12345678', description: 'Input the id of the vpc', name: 'VPC_ID'), string(defaultValue: '10.0.0.0/16', description: 'Replace with the VPC CIRD', name: 'NETWORK_CIDR'), string(defaultValue: 'subnet-27bfkste542fdf82f,subnet-0bc9b753kwy6a535', description: 'Set to use shared subnets', name: 'SUBNET_IDS')])])
            }
    }
}
