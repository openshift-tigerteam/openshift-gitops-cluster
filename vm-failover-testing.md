# testing


```shell
watch -n1 'echo "--- nodes"; oc get nodes; echo -e "\n--- vmi"; oc get vmi -A -o wide | grep -E "NAME|$NODE_NAME"; echo -e "\n--- snr"; oc get selfnoderemediation -A'
```

46
53

added kube-controller manager patch 30s
