## HA Redis on OpenShift

The following document describes the deployment of a reliable, multi-node Redis on Openshift.  It deploys a master with replicated slaves, as well as replicated redis sentinels which are use for health checking and failover.

### Configure

oc new-project foo
oc create serviceaccount redis
oc create role redis-role --verb=get,list,watch,patch --resource=pods
oc create rolebinding redis-rb --role=redis-role --serviceaccount=foo:redis

Now either import the template or deploy:
oc process -f https://raw.githubusercontent.com/pverbist/redis/master/openshift/deploy.yaml | oc create -f -

### Note:
If by any chance you have 2 masters running, kill one of them and I would suggest to kill the sentinel pods as well.
