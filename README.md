# ensf400-lab8-kubernetes-2

## Objectives
This lab will teach us the scheduling, configmaps, canary and blue-green deployment strategies of Kubernetes. Through Minikube, a simplified Kubernetes engine running on a single computer, we practice the key concepts and usage of Kubernetes.

## Environment

### Set Up Your GitHub CodeSpaces Instance

Same as Lab 6, this lab will be performed in [GitHub CodeSpaces](https://github.com/codespaces). Create an instance using GitHub Codespaces. Choose repository `denoslab/ensf400-lab8-kubernetes-2`.


```bash
$ minikube start --nodes 3 -p ensf400
```

This step will start the Minikube service with 3 virtual nodes, stored in a profile called `ensf400`. If for some reason your Codespaces instance was stopped (e.g., not using it for a while). You can restart the minikube service using this profile by running:

```bash
$ minikube start -p ensf400
```

## Steps

Go to Section 7 - 10 and complete the steps for each section. The steps can be found in the `README.md` files in each subdirectory.

## Have Your Work Checked By a TA

The TA will check the completion of the following tasks:

- Output of Section 7.
- Output of Section 8.
- Output of Section 9.
- Output of Section 10.


Each member of the group should be able to answer all of the following questions. The TA will ask each person one question selected at random, and the student must be able to answer the question to get credit for the lab.

- Q1: Explain the scheduling strategy of Node Affinity and the scenarios to use it.
    - The scheduling strategy of Node Affinity is to schedule pods only to specific subsets of nodes. It allows you to constrain which nodes is eligible to be scheduled on, based on the labels on the node.
    - This is useful to ensure pods are scheduled on particular nodes with specific hardware or software.

- Q2: Explain the scheduling strategy of Pod Anti-Affinity and the scenarios to use it.
    - The strategy is to tell the scheduler to not place a pod with particular label onto a node that contains a pod with the same label. This helps ensure that certain pods dont run on the same node as other pods.
    - This is useful to increase the size of the point of failure, and decrease the likeliness for multiple nodes to go down all at once than for a single node to go down.

- Q3: Explain the deployment strategy of blue-green deployment. How to switch between the two versions of deployments?
    - kubectl apply -f blue.yml
    - kubectl apply -f green.yml
    - kubectl patch service myapp -p '{"spec":{"selector":{"app": "green"}}}'

    - With blue.yml and green.yml file in the directory, we are able to 'kubect1 apply' the yaml files to deploy the blue and green pod. And using the kubect1 patch service command we are able to switch pods depending on the pod specified in the spec selecteor dictionary. In this case we have "app": "gree" which means we are switching from app to green pod.

- Q4: Explain the deployment strategy of canary deployment. How to adjust the ratio of users getting serviced by the canary deployment?
    - Route user traffic such that you can compare, test, and observe the behaviour of any update for a small percentage of users. It is usefull for testing tweaks, updates, or entirely new deployments.
    - To adjust the ratio of users, simply adjust the value of canary-weight in the ingress yaml file to the percentage of traffic to be routed.