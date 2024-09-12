I have created a local Kubernetes cluster with kind.
Following are changes you need to get metric-server running on Kind.

Deploy latest metric-server release. 

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.5.0/components.yaml
```

Within existing arguments to metric-server container, you need to add argument ` --kubelet-insecure-tls`.

You can create file `metric-server-patch.yaml` with following content, 
```yaml
spec:
  template:
    spec:
      containers:
      - args:
        - --cert-dir=/tmp
        - --secure-port=443
        - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
        - --kubelet-use-node-status-port
        - --metric-resolution=15s
        - --kubelet-insecure-tls
        name: metrics-server
```

NOTE: If you are using metric-server latest release above 0.5.0, it's possible container arguments may change. You should get existing arguments to container and just add ` --kubelet-insecure-tls` argument to get patch.


Patch `metric-server` deployment,

```bash
kubectl patch -n kube-system deployment metrics-server --type=json \
  -p '[{"op":"add","path":"/spec/template/spec/containers/0/args/-","value":"--kubelet-insecure-tls"}]'
```