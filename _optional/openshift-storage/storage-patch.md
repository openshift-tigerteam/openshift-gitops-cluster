
https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.19/html/troubleshooting_openshift_data_foundation/changing-resources-for-the-openshift-data-foundation-components_rhodf#changing_the_cpu_and_memory_resources_on_the_rook_ceph_pods

oc get deployments --all-namespaces -o custom-columns=NAMESPACE:.metadata.namespace,NAME:.metadata.name,CPU_REQUEST:.spec.template.spec.containers[*].resources.requests.cpu --sort-by='.spec.template.spec.containers[0].resources.requests.cpu'

oc get deployments -n openshift-storage -o custom-columns=NAMESPACE:.metadata.namespace,NAME:.metadata.name,CPU_REQUEST:.spec.template.spec.containers[*].resources.requests.cpu,CPU_LIMIT:.spec.template.spec.containers[*].resources.limits.cpu --sort-by='.spec.template.spec.containers[0].resources.requests.cpu'

```shell
oc patch -n openshift-storage storagecluster ocs-storagecluster \
    --type merge \
    --patch '{
        "spec": {
            "resources": {
                "osd": {
                    "limits": {"cpu": "1500m"},
                    "requests": {"cpu": "250m"}
                },
                "rgw": {
                    "limits": {"cpu": "1"},
                    "requests": {"cpu": "250m"}
                },
                "mgr": {
                    "limits": {"cpu": "1"},
                    "requests": {"cpu": "250m"}
                },
                "mds": {
                    "limits": {"cpu": "1"},
                    "requests": {"cpu": "250m"}
                }
            }
        }
    }'
```