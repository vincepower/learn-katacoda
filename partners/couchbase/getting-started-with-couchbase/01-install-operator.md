This tutorial provides instructions for deploying Couchbase into the environment

### Logging in to the Cluster via OpenShift CLI

Before creating any applications, login as admin. This will be required if you want to log in to the web console and use it.

To login to the OpenShift cluster from the _Terminal_ run:

``oc login -u admin -p admin``{{execute}}

This will log you in using the credentials:

* **Username:** ``admin``
* **Password:** ``admin``

Use the same credentials to log into the web console.

### Creating your own namespace

To create a new (project) namespace called ``kafka`` for the AMQ Streams Kafka Cluster Operator run the command:

``oc new-project couchbase``{{execute}}

### Install AMQ streams operator

Couchbase provides an Operator for running on OpenShift.

Deploy the Operator Lifecycle Manager Operator Group and Susbcription to easily install the operator in the previously created namespace:

``oc -n couchbase apply -f /opt/operator-install.yaml``{{execute}}

You should see the following result:

```bash
operatorgroup.operators.coreos.com/couchbase-operatorgroup created
subscription.operators.coreos.com/couchbase-streams created
```

> You can also deploy the Couchbase operator from the OpenShift OperatorHub from within the administration console.

### Check operator deployment

Follow up the operator deployment to validate it is running.

To watch the pods status run the following command:

``oc -n kafka get pods -w``{{execute}}

You will see the status of the operator changing until it gets to `running`. It should look similar to the following:

```bash
NAME                    READY   STATUS              RESTARTS   AGE
couchbase-operator-8ptlz   1/1     Running             0          34s
```

Hit <kbd>Ctrl</kbd>+<kbd>C</kbd> to stop the process.

`^C`{{execute ctrl-seq}}
