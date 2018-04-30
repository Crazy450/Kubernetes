# Kubernetes

Will be using this repository to document the steps I took to build a Kubernetes cluster on AWS  
[Kops Getting started](https://kubernetes.io/docs/getting-started-guides/kops/)  
[Kops Cluster Build Example](https://github.com/kubernetes/kops/blob/master/docs/examples/kops-tests-private-net-bastion-host.md)  

You must have configured the access key for aws within /home/Username/.aws/credentials   
[default]  
aws_access_key_id = XXXXXXXXXX  
aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXX  

You must also have ssh keys configured on your workstation

### Create a Kubernetes cluster  
kops create cluster --yes --networking=kopeio-vxlan --zones=ca-central-1a,ca-central-1b --topology=private --bastion --master-count=3 --node-count=4 kube.crazysantos.com  

You may also add the following 2 variables if you would like to specify custom node sizes:  
--node-size=t2.micro --master-size=t2.micro  

If you would like to output your kops cluster config into terraform add the following:  
 --out=.  --target=terraform  

### Verify the cluster status:  
to verify the cluster status, use the following command:  
kops validate cluster  

### Once the cluster is Up, you should also installed the Dashboard to provide a GUI interface:
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml

### Logging
Logging stack can be EFK ElasticSearch FluentD Kibana or you can replace FluentD by fluent Bit. 

[EFK FluentBit](https://akomljen.com/get-kubernetes-logs-with-elasticsearch-fluentbit-and-kibana-in-5-minutes/)  
