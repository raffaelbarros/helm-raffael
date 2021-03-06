# Rancher Istio

Our [Istio](https://istio.io/) installer wraps the istioctl binary commands in a handy helm chart, including an overlay file option to allow complex customization. It also includes:
* **[Kiali](https://kiali.io/)**: Used for graphing traffic flow throughout the mesh
* **[Jaeger](https://www.jaegertracing.io/)**: A quick start, all-in-one installation used for tracing distributed system. This is not production qualified, please refer to jaeger documentation to determine which installation you may need instead.

For more information on how to use the feature, refer to our [docs](https://rancher.com/docs/rancher/v2.x/en/istio/v2.5/).
## Known Issues

#### Airgapped Environments
If you are using this chart in an airgapped environment, you will not be able to upgrade. This is because the `istioctl` upgrade command reaches out to an external repo and it is not configurable. We are tracking the fix for this issue [here](https://github.com/rancher/rancher/issues/33402)

## Deprecations

#### v1alpha1 security policies
As of 1.6, Istio removed support for `v1alpha1` security policies resource and replaced the API with `v1beta1` authorization policies. https://istio.io/latest/docs/reference/config/security/authorization-policy/

If you are currently running rancher-istio <= 1.7.x, you need to migrate any existing `v1alpha1` security policies to `v1beta1` authorization policies prior to upgrading to the next minor version.

> **Note:** If you attempt to upgrade prior to migrating your policy resources, you might see errors similar to:
```
Error: found 6 CRD of unsupported v1alpha1 security policy
```
```
 Error: found 1 unsupported v1alpha1 security policy
 ```
 ```
 Control Plane - policy pod - istio-policy - version: x.x.x does not match the target version x.x.x
 ```
 Continue with the migration steps below before retrying the upgrade process.

##### Migrating Resources:
Migration steps can be found in this [istio blog post](https://istio.io/latest/blog/2021/migrate-alpha-policy/ "istio blog post").

You can also use these [quick steps](https://github.com/rancher/rancher/issues/34699#issuecomment-921995917 "quick steps") to determine if you need to follow the more extensive migration steps.
