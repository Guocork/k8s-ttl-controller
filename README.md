# k8s-ttl-controller

The k8s-ttl-controller project is a Kubernetes controller which provides time to live (TTL) mechanism for Kubernetes resources. The TTL behavior for each resource is configured through a `TTLPolicy` using the following user-defined parameters:
* `expirationFrom` - the resource property used as reference point from which expiration is calculated. Defaults to the resource's creation time if not specified
* `ttlFrom` the resource property used as the TTL value

## Installation

Install the CRD using:
```bash
kubectl apply -f https://raw.githubusercontent.com/fpetkovski/k8s-ttl-controller/0.4.0/deploy/crds.yaml
```
and the controller using:
```bash
kubectl apply -f https://raw.githubusercontent.com/fpetkovski/k8s-ttl-controller/0.4.0/deploy/controller.yaml
```

## Example usage

Expiring Kubernetes jobs in the `Completed` state can be done by creating a `TTLPolicy` with the following configuration:
```yaml
apiVersion: fpetkovski.io/v1alpha1
kind: TTLPolicy
metadata:
  name: jobs-ttl-controller
spec:
  resource:
    apiVersion: batch/v1
    kind: Job
  expirationFrom: .status.completionTime 
  ttlFrom: .metadata.annotations.ttl
```

Please refer to the [examples](https://github.com/fpetkovski/k8s-ttl-controller/tree/main/examples) folder for more usage patterns.

## License
[MIT](https://choosealicense.com/licenses/mit/)