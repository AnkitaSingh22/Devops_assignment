## Devops_assignment : 

This solution deploys a highly-available [**Elasticsearch (ES)**](https://www.elastic.co/what-is/elasticsearch) cluster on [**Kubenetes cluster provided by Cloud provider AWS**](https://docs.aws.amazon.com/eks/latest/userguide/clusters.html).


### _Prerequisites_

#### To create Kuberenetes cluster 
Before starting this solution, you must install and configure the following tools and resources that you need to create and manage an Amazon EKS cluster.

**kubectl** – A command line tool for working with Kubernetes clusters. This guide requires that you use version 1.21 or later. For more information, see [Installing kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html).

**eksctl** – A command line tool for working with EKS clusters that automates many individual tasks. This guide requires that you use version 0.61.0 or later. For more information, see [The eksctl command line utility](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html).

***Required IAM permissions** – I am using admin creadentials to create the cluster. Otherwise the IAM security principal that you're using must have permissions to work with Amazon EKS IAM roles and service linked roles, AWS CloudFormation, and a VPC and related resources. 

### _Getting started_

1) Installed eksctl using below commands :

 ```
 curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
 sudo mv /tmp/eksctl /usr/local/bin
 eksctl version
 ```

2) Created Kubertnetes cluster named 'my-cluster' with 3 nodes as follows to make sure standard functionality of elasticsearch application :

 `eksctl create cluster --name my-cluster --with-oidc --ssh-access --ssh-public-key esKeypair --managed --nodes 3`
 
 Note : Keep a ssh public [key-pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#prepare-key-pair) ready to connect with AWS nodes after cluster is created. In this case "esKeypair" is used.

3) Used kebernetes manifest file to deploy elasticserach cluster on my-cluster
  
   `kubectl apply -f elasticsearch-cluster.yaml`

After this we should have elasticsearch cluster deployed. We can check the resources deployed using below command :

` kubectl get all`

Output :

`````````````
NAME                         READY   STATUS    RESTARTS   AGE
pod/elasticsearch-master-0   1/1     Running   0          6h39m
pod/elasticsearch-master-1   1/1     Running   0          6h20m
pod/elasticsearch-master-2   1/1     Running   0          6h39m

NAME                                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
service/elasticsearch-master            ClusterIP   10.100.22.136   <none>        9200/TCP,9300/TCP   6h39m
service/elasticsearch-master-headless   ClusterIP   None            <none>        9200/TCP,9300/TCP   6h39m
service/kubernetes                      ClusterIP   10.100.0.1      <none>        443/TCP             42h

NAME                                    READY   AGE
statefulset.apps/elasticsearch-master   3/3     6h39m

`````````````

We can check the running ES cluster on local browser by forwarding the ports using below commands :

`kubectl port-forward svc/elasticsearch-master 9200:9200`

You should see something like this in the browser :

````````````````
{
  "name" : "elasticsearch-master-2",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "OzdNpENqSE-OGsq2JQIOyQ",
  "version" : {
    "number" : "7.14.0",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "dd5a0a2acaa2045ff9624f3729fc8a6f40835aa1",
    "build_date" : "2021-07-29T20:49:32.864135063Z",
    "build_snapshot" : false,
    "lucene_version" : "8.9.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
````````````````

### _Conclusion_ 

This is a simplistic approach to deploy elaticsearch cluster suitable for lighter workload and can be tuned based on the requirement.