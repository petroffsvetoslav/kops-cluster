pipeline {
    agent any
    stages {
        stage('Setup parameters') {
            steps {
                script {
                    properties([
                        parameters([
                            string(name: 'KOPS_STATE_STORE', defaultValue : 's3://my-state-store', description: "S3 bucket that will store the state"),
                            string(name: 'CLUSTER_NAME', defaultValue : 'cluster.k8s.local', description: "Cluster name"),
                            string(name: 'VPC_ID', defaultValue : 'vpc-12345678', description: "The VPC to use"),
                            string(name: 'SUBNET_IDS', defaultValue : 'subnet-27bfkste542fdf82f,subnet-0bc9b753kwy6a535', description: "Shared subnets to use"),
                            string(name: 'MASTER_SIZE', defaultValue : 'c5.large', description: "Instance type for the master"),
                            string(name: 'NODE_SIZE', defaultValue : 'm5.large', description: "Instance type for the nodes"),
                            string(name: 'NODE_COUNT', defaultValue : '2', description: "The number of worker nodes"),
                            string(name: 'ZONES', defaultValue : 'eu-central-1,us-east-1b', description: "Zones in which to run the cluster")
                            // string(
                            //     defaultValue: '10.0.0.0/16',
                            //     name: 'NETWORK_CIDR',
                            //     trim: true
                            // )
                        ])
                    ])
                }
            }
        }
        stage('Create cluster') {
            steps {
                sh 'echo "Saving cluster template to cluster.yaml"'
                sh 'kops create cluster --state $KOPS_STATE_STORE --name $CLUSTER_NAME --vpc $VPC_ID --subnets $SUBNET_IDS --master-size $MASTER_SIZE --node-size $NODE_SIZE --node-count $NODE_COUNT --zones $ZONES --dry-run -oyaml > cluster.yaml'
            }
        }
        stage('Deploy cluster') {
            steps {
                timeout(time: 5, unit: "MINUTES") {
                    input message: 'Do you want to approve the deploy?', ok: 'Yes'
                            }
                sh 'echo "deploying cluster from template file cluster.yaml"'
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

//  kops create man
// https://github.com/kubernetes/kops/blob/master/docs/cli/kops_create_cluster.md
