
# Semantic Kubernetes

## Recap

### Concept

> What is ~~Physics~~ Kubernetes?

**Core concepts**:

- _Actual State_ ⇦ <sub>analyze</sub> ⇦ **Reconciler**
- _Definition_ ⇦ <sub>watch</sub> ⇦ **Reconciler**
- **Reconciler** ➡ <sub>produce</sub> ➡ _Desired State_

### Implementation

> How is Kubernetes implemented?

- **etcd** holds the _Definition_
  > etcd is a distributed reliable key-value store for the most critical data of a distributed system, with a focus on being:
  >  - Simple: well-defined, user-facing API (gRPC)
  >  - Secure: automatic TLS with optional client cert authentication
  >  - Fast: benchmarked 10,000 writes/sec
  >  - Reliable: properly distributed using Raft
- **Controller** implements _Reconciling_
  https://github.com/kubernetes/kubernetes/blob/master/pkg/controller/deployment/deployment_controller.go
  ```golang
  // Run begins watching and syncing.
  func (dc *DeploymentController) Run(workers int, stopCh <-chan struct{}) {
  	defer utilruntime.HandleCrash()
  	defer dc.queue.ShutDown()

  	klog.Infof("Starting deployment controller")
  	defer klog.Infof("Shutting down deployment controller")

  	if !cache.WaitForNamedCacheSync("deployment", stopCh, dc.dListerSynced, dc.rsListerSynced, dc.podListerSynced) {
  		return
  	}

  	for i := 0; i < workers; i++ {
  		go wait.Until(dc.worker, time.Second, stopCh)
  	}

  	<-stopCh
  }
  ```

- **State** can be anything really

  :rainbow::mailbox::lock:

### Implementation Details

> what are you not telling me?

- Central to each cluster is a **Kubernetes Control Plane**

  Consists of _Kubernetes Master_, _kubelet_, _etcd_, _Controller_, **Kubernetes API**, ...

- **Kubernetes API**

  Kubernetes API is the central interface for all interacting with **API resource** defintions

  > The Kubernetes API is a resource-based (RESTful) programmatic interface provided via HTTP. It supports retrieving, creating, updating, and deleting primary resources via the standard HTTP verbs (POST, PUT, PATCH, DELETE, GET), includes additional subresources for many objects that allow fine grained authorization (such as binding a pod to a node), and can accept and serve those resources in different representations for convenience or efficiency. It also supports efficient change notifications on resources via “watches” and consistent lists to allow other components to effectively cache and synchronize the state of resources.

  Kubernetes API is strongly typed.

  Example:
  ```
  GET /api/v1/namespaces/test/pods?watch=1&resourceVersion=10245

  {
    "type": "ADDED",
    "object": {"kind": "Pod", "apiVersion": "v1", "metadata": {"resourceVersion": "10596", ...}, ...}
  }
  ```
  It also enables you to watch for changes to API resources.



