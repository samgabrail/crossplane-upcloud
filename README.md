# Using Crossplane with UpCloud

This repository contains two demos on how to use Crossplane to provision and manage resources on UpCloud.

## Prerequisites

*   A Kubernetes cluster
*   `kubectl` installed
*   Your UpCloud API credentials

### Installing Crossplane v2.0

1.  Add the Crossplane Helm repository:
    ```
    helm repo add crossplane-stable https://charts.crossplane.io/stable
    ```
2.  Update your Helm repository:
    ```
    helm repo update
    ```
3.  Install the Crossplane Helm chart:
    ```
    helm install crossplane --namespace crossplane-system --create-namespace crossplane-stable/crossplane
    ```
4.  Verify the installation:
    ```
    kubectl get pods -n crossplane-system
    ```


## Demo 1: Managed Resources

This demo shows how to deploy UpCloud resources directly using Crossplane managed resources.

### Files

The files for this demo are in the `managed-resources-demo` directory.

*   `provider.yaml`: Installs the UpCloud provider.
*   `providerconfig.example.yaml`: An example of how to configure the UpCloud provider with your API credentials.
*   `network.yaml`: Defines a network on UpCloud.
*   `server.yaml`: Defines a server on UpCloud.

### How to run

1.  Apply the `provider.yaml` file to install the UpCloud provider:
    ```
    kubectl apply -f managed-resources-demo/provider.yaml
    ```
2.  Create a `providerconfig.yaml` file by copying the example:
    ```
    cp managed-resources-demo/providerconfig.example.yaml managed-resources-demo/providerconfig.yaml
    ```
3.  Update the `managed-resources-demo/providerconfig.yaml` file with your UpCloud API credentials. This file is ignored by Git.
4.  Apply the `providerconfig.yaml` file:
    ```
    kubectl apply -f managed-resources-demo/providerconfig.yaml
    ```
5.  Apply the `network.yaml` file to create the network:
    ```
    kubectl apply -f managed-resources-demo/network.yaml
    ```
6.  Apply the `server.yaml` file to create the server:
    ```
    kubectl apply -f managed-resources-demo/server.yaml
    ```

## Demo 2: Composition with XRD (Crossplane v2)

This demo shows how to use a Composition with an XRD to create a custom API for provisioning an UpCloud server and its network, following Crossplane v2.0 conventions.

### Files

The files for this demo are in the `composition-demo` directory.

*   `xrd.yaml`: Defines the `CompositeUpCloudServer` custom resource with a `Namespaced` scope.
*   `composition.yaml`: Defines the composition of the `CompositeUpCloudServer`.
*   `composite-resource.yaml`: Creates an instance of the `CompositeUpCloudServer` directly in a namespace.

### How to run

1.  Apply the `xrd.yaml` file to define the custom resource:
    ```
    kubectl apply -f composition-demo/xrd.yaml
    ```
2.  Apply the `composition.yaml` file to define the composition:
    ```
    kubectl apply -f composition-demo/composition.yaml
    ```
3.  Apply the `composite-resource.yaml` file to create the server and network:
    ```
    kubectl apply -f composition-demo/composite-resource.yaml
    ```
