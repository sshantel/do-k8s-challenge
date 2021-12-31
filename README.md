# Name of Project
I chose the following [Digital Ocean challenge](https://www.digitalocean.com/community/pages/kubernetes-challenge):

> Deploy a log monitoring system
So your applications produce logs. Lots of logs. How are you supposed to analyze them? A common solution is to aggregate and analyze them using the ELK stack, alongside fluentd or fluentbit.

# do-k8s-challenge 

First, I created a Kubernetes Cluster via [Digital Ocean's Control Panel](https://docs.digitalocean.com/products/kubernetes/how-to/create-clusters/).

Then, I download/connect to Kubernetes `brew install kubectl` and install doctl, the official CLI for Digital Ocean API. `brew install doctl`, then `doctl auth init`, which prompts you to authenticate doctl for use with your DigitalOcean account. Next, generate [Personal Access Token]
(https://cloud.digitalocean.com/account/api/tokens)

In order to use kubectl in any cirumstance, you must configure your cluster. In K8s, a `context` is used to group access parameters under a name. The configuration for every cluster will contain a stanza for contexts with cluster-specific values which look like this:

```
contexts:
- context:
    cluster: do-sfo2-example-cluster-01
    user: do-sfo2-example-cluster-01-admin
  name: do-sfo2-example-cluster-01
current-context: do-sfo2-example-cluster-01


![](imgs/DO_k8s.png)



```

`doctl kubernetes cluster kubeconfig save <your_cluster_name>` automatically adds your config file to `~/.kube/config`

```
Cmd: $ doctl kubernetes cluster kubeconfig save k8s-1-21-5-do-0-sfo3-1640339365671
Notice: Adding cluster credentials to kubeconfig file found in "/Users/CYip/.kube/config"
Notice: Setting current-context to do-sfo3-k8s-1-21-5-do-0-sfo3-1640339365671
```

Now you're all set to use kubectl!

Now onto the fun logging stuff! First, I created a namespace called `kube-logging`. Then, I create the ElasticSearch StatefulSet, which 
manages the deployment and scaling of a set of pods. Elasticsearch is defined as a `Service` here, in the `kube-logging` namespace we just created. 









# Resources

- https://www.digitalocean.com/community/tutorials/how-to-set-up-an-elasticsearch-fluentd-and-kibana-efk-logging-stack-on-kubernetes
- https://dev.to/amitsaha/how-to-set-up-log-forwarding-in-a-kubernetes-cluster-using-fluent-bit-3bgk
