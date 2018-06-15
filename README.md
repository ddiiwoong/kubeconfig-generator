# kubeconfig-generator
Kubeconfig Generator

Prerequisite
------------

* kubernetes : 1.7+
* kubectl

Usage
-----
```
git clone https://github.com/ddiiwoong/kubeconfig-generator.git
cd kubeconfig-generator
chmod +x kubeconfig.sh
./kubeconfig.sh <service_account_name> <namespace>
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