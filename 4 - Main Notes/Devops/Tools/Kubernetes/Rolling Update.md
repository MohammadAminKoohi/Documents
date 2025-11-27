
2025-11-19 10:28

Tags: #Kubernetes 

# What is Rolling Update
Rolling update is the default deployment strategy in Kubernetes. It ensures that your application is updated gradually, by replacing old instances with new ones in a controlled manner.

### How it works:

1. **Pod Replacement:** Kubernetes replaces old pods with new ones, one at a time.
2. **Gradual Rollout:** It ensures that a specified number of new pods are available and healthy before terminating old ones.
3. **Controlled Progress:** The rollout is managed by controlling parameters like `maxUnavailable` and `maxSurge`.


![[1_LgQh-4fxXIIb-BIsN-H0OQ.gif]]


### Parameters

- **max Unavailable**: Specifies the maximum number or percentage of pods that can be unavailable during the update. Default is **25%**. This means that during the update, at least **75%** of the desired number of pods must be available.
- **max Surge**: Specifies the maximum number or percentage of pods that can be created above the desired number of pods. Default is **25%**. This means that during the update, there can be at most **125%** of the desired number of pods.