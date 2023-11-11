# kubernetes-challenges

## challenge 1

Following issues can't be fixed.

- There are some errors during gem installation in initcontainer. It is hard to fix. 
- Tried the following 3 ways for command in initcontainer, all don't work
  - ```yaml
    command: 
    - sh 
    - -c 
    - jekyll new /site
    ```
  - command: ["jekyll", "new", "/site"]
  - ```yaml
    command:
        - jekyll
        - new
        - /site
    ```  

## challenge 2

```bash
# hidden requirements: nodePort 31200
sed -i 's/ca-authority/ca/g' /etc/kubernetes/manifests/kube-apiserver.yaml
sed -i 's/6433/6443/g' /root/.kube/config

k -n kube-system get deployment  coredns -o yaml |\
 sed  's/kubedns:1.3.1/coredns\/coredns:v1.8.6/g' |\
 kubectl apply -f -

ssh node01 "systemctl status kubelet"
kubectl uncordon node01
cd /media
scp * node01:/web
```

## challenge 3

Hidden requirements:

- containerPort in db pod
- POSTGRES_USER and POSTGRES_PASSWORD

## References: 
- https://github.com/kodekloudhub/kubernetes-challenges
- https://kodekloud.com/courses/kubernetes-challenges/