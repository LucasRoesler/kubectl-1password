# Kubernetes Configuration Manager

This bash script manages Kubernetes configurations stored in 1Password. It allows you to generate and merge kubeconfig files for different contexts.

## Prerequisites

## Tools
- 1Password CLI (`op`) installed and authenticated
- `jq` installed for JSON parsing
- `kubectl` installed for managing Kubernetes clusters

## 1Password Item Structure

### Required Fields

- `server` (string): The URL of the Kubernetes API server.
- `certificate-authority-data` (string): The base64-encoded certificate authority data for the Kubernetes cluster.
- `client-certificate-data` (string): The base64-encoded client certificate data for authentication.
- `client-key-data` (string): The base64-encoded client key data for authentication.

### Optional Fields

- `context-name` (string): The desired name for the Kubernetes context. If not provided, the item title will be used as the context name.
- `default_namespace` (string): The default namespace to use for the Kubernetes context. If not provided, the "default" namespace will be used.
- `full_kubeconfig` (string): If present, this field should contain the complete kubeconfig YAML content. When this field is provided, the script will use its value instead of generating the kubeconfig from other fields.

### Additional Requirements

- The 1Password item should have a tag named `kubeconfig_cred_for_sourcing` to be recognised by the script.


## Usage

### Preparing Kubeconfig Files

Run this commands to retrieve all kubeconfigs from 1Password tagged with `kubeconfig_cred_for_sourcing` tag:

```bash
./_kube-helper.sh prep-contexts
```
This will take all the available kubeconfig items in 1Password and prepare your contexts.


After preparing your kube/config use `kubectl` as usual. From now on itr will retrieve its auth creds from 1password.