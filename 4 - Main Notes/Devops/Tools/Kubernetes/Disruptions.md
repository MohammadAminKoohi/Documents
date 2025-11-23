
2025-11-18 19:34

Tags: #Kubernetes 

# What are Disruptions?

If you want to build a highly available application, you need to know what kind of Disruptions can happen to pods.

## Voluntary and involuntary disruptions
Pods do not disappear until someone (a person or a controller) destroys them, or there is an unavoidable hardware or system software error.

We call these unavoidable cases _involuntary disruptions_ to an application. Examples are:

- a hardware failure of the physical machine backing the node
- cluster administrator deletes VM (instance) by mistake
- cloud provider or hypervisor failure makes VM disappear
- a kernel panic
- the node disappears from the cluster due to cluster network partition
- eviction of a pod due to the node being [out-of-resources](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/).

We call other cases _voluntary disruptions_. These include both actions initiated by the application owner and those initiated by a Cluster Administrator. Typical application owner actions include:

- deleting the deployment or other controller that manages the pod
- updating a deployment's pod template causing a restart
- directly deleting a pod (e.g. by accident)

Cluster administrator actions include:

- [Draining a node](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/) for repair or upgrade.
- Draining a node from a cluster to scale the cluster down (learn about [Node Autoscaling](https://kubernetes.io/docs/concepts/cluster-administration/node-autoscaling/)).
- Removing a pod from a node to permit something else to fit on that node.


# Pod Disruption Budget

This kubernetes feature helps you to create highly available applications even when you have frequent voluntary disruptions.

This feature allows you to to create a PDB object for each application that can limit the number of Pods of a replicated application that are down simultaneously from voluntary disruptions.
