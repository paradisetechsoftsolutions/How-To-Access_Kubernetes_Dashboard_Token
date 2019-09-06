# How-To-Access_Kubernetes_Dashboard_Token
## Uses of Kubernetes Dashboard
<ol>
  
<li>The dashboard provides an overview of the pods/clusters that runs on your machine. Moreover, it tells the creation and modification of individual Kubernetes resources, eg. deployments, jobs, etc. It provides accurate information on the state of Kubernetes resources in your cluster, and on any errors that may have occurred.</li></br>

<strong>$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml</strong></br>  

![1](https://user-images.githubusercontent.com/39157936/64402636-44875300-d093-11e9-87f5-1ef60965d0dd.png)  


The above command is used to connect the dashboard. Wait for Kubernetes-dashboard-x pods to goes “Running” status.</br>

<li>Once the Kubernetes-dashboard-x container goes to the “Running” state, then we can initiate a kubectl proxy with the below-given command.If you want to start only in localhost then you can change the address option to the localhost.
$ kubectl proxy --address=0.0.0.0</li>  

![2](https://user-images.githubusercontent.com/39157936/64402638-451fe980-d093-11e9-89a8-6fbec046520f.png)  


Now open the below Kubernetes dashboard URL in a browser.</br></br>
<strong>http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/.</strong></br>

The given link will direct you to the Kubernetes dashboard. Here, to build a connection we need a token (key). And the key will be explained to you by the below commands.</br>  

![3](https://user-images.githubusercontent.com/39157936/64402639-451fe980-d093-11e9-963b-665c3f7bf099.png)  



<li>To login properly into the Kubernetes dashboard, we need to create a service account and assign the proper role.</li>
<strong>$ kubectl create service account dashboard -n default</strong>  

 ![4](https://user-images.githubusercontent.com/39157936/64402641-451fe980-d093-11e9-8a4e-9fb505b89903.png)  
 

<strong>$ kubectl create clusterrolebinding dashboard-admin -n default --clusterrole=cluster-admin --serviceaccount=default:dashboard</strong></br>  

 ![5](https://user-images.githubusercontent.com/39157936/64402642-45b88000-d093-11e9-9c09-097540c6ae70.png)  
 
</br>
Now the password to login Kubernetes dashboard can be viewed by running the below command. Copy the decoded password and login to the dashboard.</br>

<strong>$ kubectl get secret $(kubectl get serviceaccount dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode</strong></br>  

![6](https://user-images.githubusercontent.com/39157936/64402643-45b88000-d093-11e9-91b6-28393a1ae72f.png)  

</br>


After putting the above command we’ll attain a token key for the access of the Kubernetes dashboard.</br>
<li>As mentioned in the below screenshot, that shows you to opt from those 2 options, i.e. Kubeconfig & Token. We prefer you to select token, and insert the key and proceed with the sign-in process.</li></br>  

![7](https://user-images.githubusercontent.com/39157936/64402644-45b88000-d093-11e9-92bf-4ebfc020d9e7.png)  


<li>After the sign-in, it will show you the dashboard main page. On that page, we can see the node’s running stage, replicas, clusters, etc. and every action that we perform on a created object. It helps us to visualize every action of master and node.</li></br>  

![8](https://user-images.githubusercontent.com/39157936/64402645-46511680-d093-11e9-9310-ec45a02a15c4.png)  


<li>Kubeadm token</br>
Bootstrap tokens are used for establishing bidirectional trust between a node joining the cluster and a control-plane node. The token generated is valid only for 24hours. In that case, the 24 hours exceed we need to generate the new token using the command:</li>
<strong>$ sudo kubeadm token create</strong></br>
The current token can be the view from the master using the below command.</br>
<strong>$ sudo kubeadm token list</strong></br>  

![9](https://user-images.githubusercontent.com/39157936/64402646-46511680-d093-11e9-8b16-a8684ac22f7f.png)
  
  </br>

We have described flannel that is used for the communication process and after the flannel network is deployed, we can verify the flannel interface for the IP address assigned.</br>

</ol>
