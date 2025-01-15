# Configure NFS For Kuberenetes

Craete A instance for external volume to save the files of worker-nodes.Install nfs package in the instance and configure a mount point with /etc/exports file.

## Configure a mount point 

To Create mount point run ;

```bash
  yum install nfs-utils -y
```
```bash
  vi /etc/exports
```
/mnt *(rw,sync,no_subtree_check,no_root_squash,no_all_squash
insecure) put enrty in the exports file and run next cmd.
```bash
  systemctl enable nfs-server --now
```
```bash
   exportfs -rav
```
```bash
  showmount -e localhost
```

## Configure a mount point on work-node machines 


```bash
  yum install nfs-utils -y
```
```bash
    systemctl enable nfs-server --now
```
```bash
   mount -t nfs 172.31.9.70:/mnt /mnt
```
run mount -t nfs command allow nfs port in both worker-node machines and nfs-volume machine and allow icmp-ipv4 in all machines for ping.
```bash
  vi /etc/fstab
```
put entry in fstab file for mount permanently
```bash
  systemctl restart nfs-server 
```
## Runs Commands on Master-node

```bash
kubectl apply -f pv-nfs.yaml
```

```bash
kubectl apply -f pvc-nfs.yaml
```

```bash
kubectl apply -f pod-nfs.yaml
```

```bash
kubectl get pods 
```
```bash
kubectl get pv 
```
```bash
kubectl get pvc
```
```bash
kubectl exec -it <podname> -- bash
```
```bash
df -h 
```
we can see mount point /mnt inside the container.
