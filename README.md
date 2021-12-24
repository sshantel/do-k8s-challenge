### WIP!

# do-k8s-challenge

I chose the following [Digital Ocean challenge](https://www.digitalocean.com/community/pages/kubernetes-challenge):

> Deploy a log monitoring system
So your applications produce logs. Lots of logs. How are you supposed to analyze them? A common solution is to aggregate and analyze them using the ELK stack, alongside fluentd or fluentbit.

# Step 1

Create Kubernetes Cluster via [Digital Ocean's Control Panel](https://docs.digitalocean.com/products/kubernetes/how-to/create-clusters/).

# Step 2

Download/Connect to Kubernetes

`brew install kubectl`

# Step 3

Install doctl, the official CLI for Digital Ocean API.

`brew install doctl`, then `doctl auth init`, which prompts you to authenticate doctl for use with your DigitalOcean account.

# Step 4

Generate Personal Access Token
https://cloud.digitalocean.com/account/api/tokens?

# Step 5

Often times, I use the `kubectl` command right away without configuring my cluster, which returns ```No version set for command kubectl```. I never fully understood why this happened, but now that I've configured my own cluster I finally understand! 

In order to use kubectl, you must configure your cluster. In K8s, a `context` is used to group access parameters under a name. The configuration for every cluster will contain a stanza for contexts with cluster-specific values which look like this:


```
contexts:
- context:
    cluster: do-sfo2-example-cluster-01
    user: do-sfo2-example-cluster-01-admin
  name: do-sfo2-example-cluster-01
current-context: do-sfo2-example-cluster-01
```


`doctl kubernetes cluster kubeconfig save <your_cluster_name>` automatically adds your config file to `~/.kube/config`


```
Cmd: $ doctl kubernetes cluster kubeconfig save k8s-1-21-5-do-0-sfo3-1640339365671
Notice: Adding cluster credentials to kubeconfig file found in "/Users/CYip/.kube/config"
Notice: Setting current-context to do-sfo3-k8s-1-21-5-do-0-sfo3-1640339365671
```

Now you're all set to use kubectl!
