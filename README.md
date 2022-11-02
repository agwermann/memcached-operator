# MemCached Operator Example

## Getting Started

You’ll need a Kubernetes cluster to run against. You can use [KIND](https://sigs.k8s.io/kind) to get a local cluster for testing, or run against a remote cluster.
**Note:** Your controller will automatically use the current context in your kubeconfig file (i.e. whatever cluster `kubectl cluster-info` shows).

### Running on the cluster

1. Create the kind cluster:

```sh
kind create cluster
```

2. Install Instances of Custom Resources:

```sh
kubectl apply -f config/samples/
```

3. Build your image to the location specified by `IMG`:

```sh
make docker-build IMG=dev.local/memcached-operator:0.1
```

4. Push your image to the location specified by `IMG` (optional):

```sh
make docker-push IMG=dev.local/memcached-operator:0.1
```

5. Deploy the controller to the cluster with the image specified by `IMG`:

```sh
make deploy IMG=dev.local/memcached-operator:0.1
```

### Uninstall CRDs

To delete the CRDs from the cluster:

```sh
make uninstall
```

### Undeploy controller

UnDeploy the controller to the cluster:

```sh
make undeploy
```

## Contributing
// TODO(user): Add detailed information on how you would like others to contribute to this project

### How it works
This project aims to follow the Kubernetes [Operator pattern](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)

It uses [Controllers](https://kubernetes.io/docs/concepts/architecture/controller/) 
which provides a reconcile function responsible for synchronizing resources untile the desired state is reached on the cluster 

### Test It Out

1. Install the CRDs into the cluster:

```sh
make install
```

2. Run your controller (this will run in the foreground, so switch to a new terminal if you want to leave it running):

```sh
make run
```

**NOTE:** You can also run this in one step by running: `make install run`

### Modifying the API definitions
If you are editing the API definitions, generate the manifests such as CRs or CRDs using:

```sh
make manifests
```

**NOTE:** Run `make --help` for more information on all potential `make` targets

More information can be found via the [Kubebuilder Documentation](https://book.kubebuilder.io/introduction.html)

## License

Copyright 2022.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Create new API Project

```sh
operator-sdk init --domain agwermann \                    
  --repo github.com/agwermann/memcached-operator

operator-sdk create api --group cache --version v1alpha1 \
  --kind Memcached --resource --controller
```

## 

```
export IMG=dev.local/memcached-operator:0.1
export NAMESPACE=memcache-demo-project

cd config/manager
kustomize edit set image controller=${IMG}
kustomize edit set namespace "${NAMESPACE}"
cd ../../

cd config/default
kustomize edit set namespace "${NAMESPACE}"
cd ../../
```

## Resources

[Building Custom Operator - Red Hat Developers](https://developers.redhat.com/blog/2020/08/21/hello-world-tutorial-with-kubernetes-operators#build_the_operator)
[Create Custom Operator - IBM Developers](https://developer.ibm.com/learningpaths/kubernetes-operators/develop-deploy-simple-operator/create-operator/)