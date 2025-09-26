# testing


```
watch -n2 'echo "---"; oc get selfnoderemediation -A; echo "---"; oc get vmi -A -o wide | grep -E "NAME|$NODE_NAME"'
```