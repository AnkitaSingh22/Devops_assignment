## Devops_assignment : 

This solution is deploys a highly-avaiable [**Elasticsearch (ES)**](https://www.elastic.co/what-is/elasticsearch) cluster on [**Kubenetes cluster provided by Cloud provider AWS**](https://docs.aws.amazon.com/eks/latest/userguide/clusters.html).


### _Prerequisites_

#### To create Kuberenetes cluster 
Before starting this solution, you must install and configure the following tools and resources that you need to create and manage an Amazon EKS cluster.

**kubectl** – A command line tool for working with Kubernetes clusters. This guide requires that you use version 1.21 or later. For more information, see [Installing kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html).

**eksctl** – A command line tool for working with EKS clusters that automates many individual tasks. This guide requires that you use version 0.61.0 or later. For more information, see [The eksctl command line utility](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html).

***Required IAM permissions** – I am using admin creadentials to create the cluster. Otherwise the IAM security principal that you're using must have permissions to work with Amazon EKS IAM roles and service linked roles, AWS CloudFormation, and a VPC and related resources. 

### _Getting started_

1) Installed eksctl using below commands :

 curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
 sudo mv /tmp/eksctl /usr/local/bin
 eksctl version

2) Create Kubertnetes cluster named 'my-cluster' with 3 nodes as follows to make sure standard functionality of elasticsearch application :

 eksctl create cluster --name my-cluster --with-oidc --ssh-access --ssh-public-key esKeypair --managed --nodes 3

3) Using kebernetes manifest file to deploy elasticserach cluster on my-cluster
  
   kubectl apply -f elasticsearch-cluster.yaml
