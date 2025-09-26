# testing


```shell
watch -n3 'echo "--- vmi ---"; oc get vmi -A -o wide | grep -E "NAME|$NODE_NAME"; echo -e "\n--- snr ---"; oc get selfnoderemediation -A'
```