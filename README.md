# Using Crossplane with UpCloud

This repository contains two demos on how to use Crossplane to provision and manage resources on UpCloud.

## Prerequisites

*   A Kubernetes cluster
*   `kubectl` installed
*   Crossplane installed in your cluster
*   Your UpCloud API credentials

## Demo 1: Managed Resources

This demo shows how to deploy UpCloud resources directly using Crossplane managed resources.

### Files

The files for this demo are in the `managed-resources-demo` directory.

*   `provider.yaml`: Installs the UpCloud provider.
*   `providerconfig.yaml`: Configures the UpCloud provider with your API credentials. **Remember to replace the placeholder credentials in this file.**
*   `network.yaml`: Defines a network on UpCloud.
*   `server.yaml`: Defines a server on UpCloud.

### How to run

1.  Apply the `provider.yaml` file to install the UpCloud provider:
    ```
    kubectl apply -f managed-resources-demo/provider.yaml
    ```
2.  Update the `providerconfig.yaml` file with your UpCloud API credentials.
3.  Apply the `providerconfig.yaml` file:
    ```
    kubectl apply -f managed-resources-demo/providerconfig.yaml
    ```
4.  Apply the `network.yaml` file to create the network:
    ```
    kubectl apply -f managed-resources-demo/network.yaml
    ```
5.  Apply the `server.yaml` file to create the server:
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
