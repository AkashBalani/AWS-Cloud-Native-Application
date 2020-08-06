# AWS-Cloud-Native-Application #

# How to Deploy Cloud Infrastructure #

1. `cd team6-infra-master`

Change the Directory to team6-infra-master

2. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-cluster"`

This will bring up the cluster
P.S This could take upto 5 - 7 minutes 

3. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-fleetman"`

This will deploy the frontend + backend + database on AWS

4. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-elastic-stack"`

P.S It is recommended that you use atleast t2.medium as t2.micro is not sufficient for elasticsearch Nodes

This will deploy an EFK (Elastic - FluentD - Kibana) Stack

5. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-monitoring-setup"`

This will install Helm + Prometheus + Grafana

6. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-jenkins"`

This will bring up Jenkins which will be used for CI/CD

7. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-slack-connection"`

This will establish a slack connection which would display Alerts through Monitoring Setup

Please Note that both Prometheus and Grafana are deployed as Load Balancers for ease of access
You can view their endpoints by the following command
`kubectl get svc -n monitoring`

For getting the Grafana Password use the following command
`kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo`

In the EFK stack, Kibana is deployed as a LoadBalancer
Please make changes if you dont want these as Load Balancers as they can incur significant charges!
To view Kibana Endpoint use the following command
`kubectl get svc -n kube-system`
