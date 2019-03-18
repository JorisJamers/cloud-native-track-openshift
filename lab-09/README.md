# Lab - 09 Rolling back applications

It's also possible to rollback your applications. Imagine that our last commit
was not successful but Openshift deployed it anyway. We can easily rollback the
deployment with the following steps.

## Task 1:  Get the current deployment configs

We will need the name of the deployment config in order to rollback the entire
deployment.

```
oc get dc

NAME            REVISION   DESIRED   CURRENT   TRIGGERED BY
scm-web-hooks   3          1         1         config,image(scm-web-hooks:latest)
```

When we know the name of the deployment we can use the name to rollback the entire
application. The output should be something like this.

```
oc rollback dc/scm-web-hooks

#4 rolled back to scm-web-hooks-2
Warning: the following images triggers were disabled: scm-web-hooks:latest
```

Check out your deployment by getting the route and browse to the `HOST/PORT`
section of the output.

```
oc get route
```

We succefully rolled back our application. If you for example tweaked the colour
of the deploy you will see that the old color is back.

## Task 2 : Delete your project

You can delete your project in the web console or via the CLI with the following
command.

```
oc delete project scm-web-hooks-${USERNAME}
```
