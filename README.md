## Devops_assignment : 

This solution is deploys a highly-avaiable [**Elasticsearch (ES)**](https://www.elastic.co/what-is/elasticsearch) cluster on [**Kubenetes cluster provided by Cloud provider AWS**](https://docs.aws.amazon.com/eks/latest/userguide/clusters.html) standard helm charts publically available for Elastic search cluster.


### _Prerequisites_

#### 1) To create Kuberenetes cluster 
Before starting this solution, you must install and configure the following tools and resources that you need to create and manage an Amazon EKS cluster.

kubectl – A command line tool for working with Kubernetes clusters. This guide requires that you use version 1.21 or later. For more information, see [Installing kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html).

eksctl – A command line tool for working with EKS clusters that automates many individual tasks. This guide requires that you use version 0.61.0 or later. For more information, see [The eksctl command line utility](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html).

Required IAM permissions – The IAM security principal that you're using must have permissions to work with Amazon EKS IAM roles and service linked roles, AWS CloudFormation, and a VPC and related resources. For more information, see Actions, resources, and condition keys for Amazon Elastic Container Service for Kubernetes and Using service-linked roles in the IAM User Guide. You must complete all steps in this guide as the same user.

#### 2) To Use helm
  Kubernetes >= 1.14
  Helm >= 2.17.0
 

### Getting started
