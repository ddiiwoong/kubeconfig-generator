# kubeconfig-generator
Kubeconfig Generator can make automatically a kubeconfig for Managed Kubernetes Service.

Prerequisite
------------

* kubernetes : 1.7+
* kubectl
* jq : (if macOS) https://stedolan.github.io/jq/download/

Usage
-----
```
git clone https://github.com/ddiiwoong/kubeconfig-generator.git
cd kubeconfig-generator
chmod +x kubeconfig.sh
./kubeconfig.sh <service_account_name> <namespace>
```

## Check a kubeconfig 
You can verify the kubeconfig below location
```
$ ls -al /tmp/kube/
total 48
drwxr-xr-x  8 ddii  wheel   256  6 15 16:29 .
drwxrwxrwt  9 root  wheel   288  6 15 16:33 ..
-rw-r--r--  1 ddii  wheel  1887  6 15 16:34 ca.crt
-rw-------  1 ddii  wheel  4052  6 14 10:34 k8s-agones-default-conf
-rw-------  1 ddii  wheel  4044  6 15 16:24 k8s-test2-default-conf
-rw-------  1 ddii  wheel  4044  6 15 16:28 k8s-test3-default-conf
-rw-------  1 ddii  wheel  4052  6 15 16:34 k8s-test99-default-conf
-rw-------  1 ddii  wheel  4092  6 15 16:17 k8s-testaccount-default-conf

$ KUBECONFIG=/tmp/kube/k8s-<service_account_name>-<namespace>-conf
$ kubectl get nodes
NAME            STATUS    ROLES     AGE       VERSION
10.178.188.11   Ready     <none>    8d        v1.10.1-2+7d2976e4bcbeb9
10.178.188.15   Ready     <none>    8d        v1.10.1-2+7d2976e4bcbeb9
10.178.188.16   Ready     <none>    8d        v1.10.1-2+7d2976e4bcbeb9
```

example
-------
```
./kubeconfig.sh test99 default
Creating target directory to hold files in /tmp/kube...done
Creating a service account: test99 on namespace: default
serviceaccount "test99" created

Getting secret of service account test99-default
Secret name: test99-token-v5v28

Extracting ca.crt from secret...done
Getting user token from secret...done
Setting current context to: dgs
Cluster name: dgs
Endpoint: https://********************

Preparing k8s-test99-default-conf
Setting a cluster entry in kubeconfig...Cluster "dgs" set.
Setting token credentials entry in kubeconfig...User "test99-default-dgs" set.
Setting a context entry in kubeconfig...Context "test99-default-dgs" modified.
Setting the current-context in the kubeconfig file...Switched to context "test99-default-dgs".
Creating RBACclusterrolebinding.rbac.authorization.k8s.io "test99-rbac" created
############# review rbac manifest ##############

apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: test99-rbac
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
subjects:
  - kind: ServiceAccount
    name: test99
    namespace: default

All done! Test with:
NAME            STATUS    ROLES     AGE       VERSION
10.178.188.11   Ready     <none>    8d        v1.10.1-2+7d2976e4bcbeb9
10.178.188.15   Ready     <none>    8d        v1.10.1-2+7d2976e4bcbeb9
10.178.188.16   Ready     <none>    8d        v1.10.1-2+7d2976e4bcbeb9
```
