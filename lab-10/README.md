# Lab - 10 Using Config Map

## Task 1 : Create a new project

Export your username environment variable.

```
export USERNAME=<username>
```

Now create the new project with the variable.

```
oc new-project configmap-${USERNAME} --display-name="Test WebHooks"
```

## Task 2 : Create an application with configmap

With a configmap we are able to easily pass environment variables to the deployment
we are creating.

Create a file ui.properties with the following content:

```
color=blue
```

This will pass an environment variable to the pods that we will create with our
deployment. We are now able to create a configmap with this file. We are also
going to pass a `from literal` and the command will look like this.

```
oc create configmap  config --from-literal=message='Hello World!' --from-file=ui.properties
```

Verify that the configmap has been created succesfully:

```
oc get configmap/config -o json

{
    "apiVersion": "v1",
    "data": {
        "message": "Hello World!",
        "ui.properties": "color=blue\n"
    },
    "kind": "ConfigMap",
    "metadata": {
        "creationTimestamp": "2019-03-18T13:40:56Z",
        "name": "config",
        "namespace": "configmap-user15",
        "resourceVersion": "55827",
        "selfLink": "/api/v1/namespaces/configmap-user15/configmaps/config",
        "uid": "75336d7c-4983-11e9-80d2-02b5fe97fb22"
    }
}
```

Copy the following `json` files to deploy the simple application with our
environment variables.

Get the `node-app-build.json` and the `node-app-deployment.json` from this repo
and apply them with the following commands.

```
oc create -f node-app-deployment.json

oc create -f node-app-build.json
```

After a while you will be able to browse to the endpoint shown on the dashboard.
You will see that we will get a blue background with the `Hello World!` message.

## Task 3 : Edit the configmap

```
oc edit configmap config
```

Edit the color to green and you a new app should be deployed with the new config.

## Task 4 : Delete your project

You can delete your project in the web console or via the CLI with the following
command.

```
oc delete project configmap-${USERNAME}
```
