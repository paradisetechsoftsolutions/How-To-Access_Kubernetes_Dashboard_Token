# How-To-Access_Kubernetes_Dashboard_Token
## Uses of Kubernetes Dashboard
<ol>
  
<li>The dashboard provides an overview of the pods/clusters that runs on your machine. Moreover, it tells the creation and modification of individual Kubernetes resources, eg. deployments, jobs, etc. It provides accurate information on the state of Kubernetes resources in your cluster, and on any errors that may have occurred.</li></br>

<strong>$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml</strong></br>  

![1](https://user-images.githubusercontent.com/39157936/64402636-44875300-d093-11e9-87f5-1ef60965d0dd.png)  


The above command is used to connect the dashboard. Wait for Kubernetes-dashboard-x pods to goes “Running” status.</br>

<li>Once the Kubernetes-dashboard-x container goes to the “Running” state, then we can initiate a kubectl proxy with the below-given command.If you want to start only in localhost then you can change the address option to the localhost.
$ kubectl proxy --address=0.0.0.0</li>

Now open the below Kubernetes dashboard URL in a browser.</br></br>
<strong>http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/.</strong></br>

The given link will direct you to the Kubernetes dashboard. Here, to build a connection we need a token (key). And the key will be explained to you by the below commands.</br>


<li>To login properly into the Kubernetes dashboard, we need to create a service account and assign the proper role.</li>
<strong>$ kubectl create service account dashboard -n default</strong>

<strong>$ kubectl create clusterrolebinding dashboard-admin -n default --clusterrole=cluster-admin --serviceaccount=default:dashboard</strong>

Now the password to login Kubernetes dashboard can be viewed by running the below command. Copy the decoded password and login to the dashboard.
$ kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode

After putting the above command we’ll attain a token key for the access of the Kubernetes dashboard.
As mentioned in the below screenshot, that shows you to opt from those 2 options, i.e. Kubeconfig & Token. We prefer you to select token, and insert the key and proceed with the sign-in process.

After the sign-in, it will show you the dashboard main page. On that page, we can see the node’s running stage, replicas, clusters, etc. and every action that we perform on a created object. It helps us to visualize every action of master and node.

Kubeadm token
Bootstrap tokens are used for establishing bidirectional trust between a node joining the cluster and a control-plane node. The token generated is valid only for 24hours. In that case, the 24 hours exceed we need to generate the new token using the command:
$ sudo kubeadm token create
The current token can be the view from the master using the below command.
$ sudo kubeadm token list

We have described flannel that is used for the communication process and after the flannel network is deployed, we can verify the flannel interface for the IP address assigned.

</ol>
