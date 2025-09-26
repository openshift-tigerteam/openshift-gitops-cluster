# testing


```
watch -n2 'oc get selfnoderemediation -A; echo "---"; oc get vmi -A -o wide | grep -E "NAME|$NODE_NAME"'
```