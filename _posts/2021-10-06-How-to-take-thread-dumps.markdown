---
layout: post
title:  "How to take thread dumps for a java service running in k8s"
date:   2021-10-06 16:39:31 +0530
comments_id: 10
---

Recently I came across this interesting problem, where I wanted to take a thread dump of a java service. Our service was restarting multiple times because of which were were not able to download the thread dump at the time of CPU outage. This blogs covered how we were finally able to get the thread dump.


We used the [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) concept from the Kubernetes.

### Concepts

* PersistentVolume: This is the actual store where we will store the data. Conceptually it is similar to nodes, i.e. we don’t actually interact much with nodes, we have an abstract concept pod built on top of it.

* PersistentVolumeClaim: We are claiming some volume. In pods, we can directly refer to the claim.


### Steps to create an link a Persistent Volume

1. Create a Persistent Volume Claim using kubectl apply -f pvc-demo.yaml.

```yaml
# pvc-demo.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-demo-2
  namespace: default
spec:
  storageClassName: standard
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 75Gi

```

2. Check that the PVC is created `kubectl get pvc --namespace default`.

3. Change the deployment config to use this PVC in the volumes section.

```yaml
 - name: heap-dumps
    persistentVolumeClaim:
    claimName: pvc-demo-2
```

4. Redeploy the service using kubectl apply -f manager.yaml.

5. Now all the data inside heapdump is preserved. 