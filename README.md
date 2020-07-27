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

This will deploy an EFK (Elastic - FluentD - Kibana) Stack

5. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-monitoring-setup"`

This will install Helm + Prometheus + Grafana

6. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-jenkins"`

This will bring up Jenkins which will be used for CI/CD

7. `ansible-playbook setup-k8s-cluster-with-webhook.yaml -vvvv --tags "create-slack-connection"`

This will establish a slack connection which would display Alerts through Monitoring Setup
