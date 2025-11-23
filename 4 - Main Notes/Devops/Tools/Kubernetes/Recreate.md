
2025-11-19 11:57

Tags: #Kubernetes 

# What is Recreate
Recreate deployment strategy involves terminating all existing instances of pods before creating new ones. It leads to downtime during the update process but ensures a clean, predictable transition.

### How it works:

1. **Pod Termination:** Kubernetes terminates all existing pods.
2. **Pod Creation:** It creates new pods with updated configurations.

### Parameters:

- Recreate strategy **doesn’t have** parameters like `maxUnavailable` or `maxSurge`.

### Real-time Use Cases:

1. **Batch Processing:** In scenarios where you have batch jobs or background tasks that can be paused temporarily, recreate strategy works well. For example, if you’re running a batch processing system where processing can be paused for a brief period, using recreate ensures a clean transition without risking data inconsistencies or job failures.

2. In a single-node cluster where the deployment’s pods consume all available resources, using the rolling update strategy may lead to issues. If the rolling update attempts to create additional pods before terminating the old ones, it can result in resource exhaustion. Since the cluster has only one node, there’s no room for extra pods, causing the update to fail.  
    In such a scenario, the recreate strategy becomes more suitable. By terminating all existing pods before creating new ones, the recreate strategy ensures that resources are freed up before new pods are launched. This allows for a smoother update process without the risk of resource exhaustion.







