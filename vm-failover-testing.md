# testing


```shell
watch -n1 'echo "--- nodes"; oc get nodes; echo -e "\n--- vmi"; oc get vmi -A -o wide | grep -E "NAME|$NODE_NAME"; echo -e "\n--- snr"; oc get selfnoderemediation -A'
```

```shell
sudo systemctl stop kubelet.service && sleep 360s && sudo systemctl start kubelet.service
```


46
53

added KubeletConfig

49