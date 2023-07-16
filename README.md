Deploying Java App on Kubernetes Cluster

This README provides step-by-step instructions for deploying a Java application on a Kubernetes cluster using EC2 instances and Kops. The deployment includes setting up the necessary infrastructure, configuring the cluster, and deploying the application using Kubernetes manifests.
Prerequisites

Before you begin, ensure that you have the following prerequisites:

    AWS Account: You need an AWS account with appropriate permissions to create EC2 instances and manage resources.
    EC2 Key Pair: Create an EC2 key pair to securely access the EC2 instances.
    AWS CLI: Install and configure the AWS Command Line Interface (CLI) on EC2 instance.
    Kubectl: Install kubectl on EC2 instance to interact with the Kubernetes cluster.
    Kops: Install kops on EC2 instance to create and manage the Kubernetes cluster.

Deployment Steps
1. Provision EC2 Instance

Launch an EC2 instance on AWS using the desired instance type and configuration. Make sure the instance is accessible from your local machine and has the necessary security group rules to allow incoming connections.

2. Install kubectl

On your local machine, install kubectl to interact with the Kubernetes cluster. You can follow the official Kubernetes documentation to install kubectl for your specific operating system.

    For Linux
    https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

3. Install kops

On your local machine, install kops to create and manage the Kubernetes cluster. You can follow the official Kops documentation to install kops for your specific operating system.

    https://kops.sigs.k8s.io/getting_started/install/

4. Create S3 Bucket for Cluster State

Before creating the Kubernetes cluster using Kops, you need to set up an S3 bucket to store the cluster state. The cluster state contains important information about the cluster configuration and is used by Kops for managing the cluster.

5. Create Kubernetes Cluster

Use kops to create a Kubernetes cluster on AWS. Use the following command as an example:

    kops create cluster --name=mycluster.k8s.local --state=s3://your-bucket-name --zones=us-east-1a,us-east-1b --master-size=t2.micro --node-count=3 --node-size=t2.micro

Replace mycluster.k8s.local with your desired cluster name and s3://your-bucket-name with the S3 bucket name where Kops will store the cluster state.

6. Update Kubernetes Cluster

After creating the cluster, you may need to update it with the desired configuration. Use the following command as an example:

    kops update cluster --name=mycluster.k8s.local --state=s3://your-bucket-name --yes --admin

7. Configure Kubernetes Deployment

Clone this directory 

    cd kubernetes
    use 
    kubectl apply -f  app/
    kubectl apply -f  db/
    kubectl apply -f  memcache/
    kubectl apply -f  tomapp/

    Check 
    kubectl get pods ### All pods must be in Running state
    Kubectl get services ### Check all services are configured and running 

Conclusion

Congratulations! You have successfully deployed your Java application on a Kubernetes cluster using EC2 instances and Kops. This README provides a high-level overview of the deployment process, and you can further customize it to include specific details and instructions relevant to your application and environment.

Remember to include any additional prerequisites, troubleshooting tips, and security considerations based on your project requirements.

