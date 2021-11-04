# Etcd helper

A helper tool for getting OpenShift/Kubernetes data directly from Etcd.

## How to build

    $ go build .

## Basic Usage

This requires setting the following flags:

* `-key` - points to `master.etcd-client.key`
* `-cert` - points to `master.etcd-client.crt`
* `-cacert` - points to `ca.crt`

Once these are set properly, one can invoke the following actions:

* `ls` - list all keys starting with prefix
* `get` - get the specific value of a key
* `put`  - put the specific value of a key
* `dump` - dump the entire contents of the etcd

## Sample Usage

Get etcd information.

```
    export ETCDCTL_CACERT="/etc/kubernetes/static-pod-resources/etcd-certs/configmaps/etcd-serving-ca/ca-bundle.crt"
    export ETCDCTL_KEY="/etc/kubernetes/static-pod-certs/resources/etcd-certs/secrets/etcd-all-certs/etcd-peer-mmcn.openlab.red.key"
    export ETCDCTL_KEY="/etc/kubernetes/static-pod-resources/etcd-certs/secrets/etcd-all-certs/etcd-peer-mmcn.openlab.red.key"
    export ETCDCTL_CERT="/etc/kubernetes/static-pod-resources/etcd-certs/secrets/etcd-all-certs/etcd-peer-mmcn.openlab.red.crt"
```

List all keys starting with `/openshift.io`:

```
./etcdhelper -key $ETCDCTL_KEY -cert $ETCDCTL_CERT -cacert $ETCDCTL_CACERT ls /openshift.io
```

Get JSON-representation of `/kubernetes.io/clusterrolebindings/system-bootstrap-node-bootstrapper`:

```
./etcdhelper -key $ETCDCTL_KEY -cert $ETCDCTL_CERT -cacert $ETCDCTL_CACERT get /kubernetes.io/clusterrolebindings/system-bootstrap-node-bootstrapper
```

Put value (JSON or YAML) to `/kubernetes.io/clusterrolebindings/system-bootstrap-node-bootstrapper`:

```
./etcdhelper -key $ETCDCTL_KEY -cert $ETCDCTL_CERT -cacert $ETCDCTL_CACERT put /kubernetes.io/clusterrolebindings/system-bootstrap-node-bootstrapper '<your value>'
```

Dump the contents of etcd to stdout:

```
./etcdhelper -key $ETCDCTL_KEY -cert $ETCDCTL_CERT -cacert $ETCDCTL_CACERT dump
```


# Reference
* https://github.com/openshift/origin/tree/master/tools/etcdhelper
