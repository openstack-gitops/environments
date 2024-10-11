# rhoso18 example overlay

When working with GitOps and Kustomize, providing overlays for specific
environments is a common practice. In this example, we provide a set of
overlays to adjust values to match a specific environment, using the
`base/compact` kustomization as an example.

The `base/compact` kustomization contains the manifests provided by Red Hat
OpenStack Services on OpenShift (RHOSO) documentation. We then provide an
overlay in the `datacenter/rhoso18` kustomization directory as an example of
how to provide an overlay construct for deploying with GitOps.

For more information about deploying RHOSO, see
https://docs.redhat.com/en/documentation/red_hat_openstack_services_on_openshift/18.0.

# Generating the example

Using the overlay directly is possible, but generating a flat manifest can help
with tracking changes between revisions and avoid surprise updates when base
layers are changed.

To generate the flat manifest, use `kustomize` to build and write the contents
to the `deployment/generated.yaml` file. When creating the GitOps Application,
reference the path to the flat manifest instead of the dynamically generated
path so that if any changes to the base are imported to the repo, then those
changes will not be immediately reflected in the deployment.

```bash
$ cd datacenter/rhoso18
$ kustomize build > deployment/generated.yaml
$ git commit -a -m "Update deployment manifests"
$ git push
```
