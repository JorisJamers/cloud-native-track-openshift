# Lab - 08 SCM Web Hooks

It's possible to trigger a deployment of an application in various ways. In this
lab we will demonstrate the deployment of an application via a GitHub Web Hook
trigger.


## Task 1 : Create a new project

Export your username environment variable.

```
export USERNAME=<username>
```

Now create the new project with the variable.

```
oc new-project scm-web-hooks-${USERNAME} --display-name="Test WebHooks"
```

## Task 2 : Create a new application

We will use a forked repository from the application used in the previous lab.
Browse to GitHub and fork the following repository https://github.com/RedHatWorkshops/bluegreen.

```
oc new-app --image-stream=php --code=https://github.com/your_github_username/bluegreen.git --name=scm-web-hooks
```

## Task 3 : Look at some of the created resources

Check out the build configuration.

```
oc get bc
```

Check out the deployment configuration.

```
oc get dc
```

Show the created service.

```
oc get service
```

Show the replication controller.

```
oc get rc
```

Show the route you have created.

```
oc get route
```

You will see that there is no route created yet for this application. This is
something we will do in the following steps of the lab.

Show the build, this could be in progress with a status `Running` or complete with
the status `Complete`. When the build is complete you will find the following output
in the logs.

```
oc logs build/scm-web-hooks-1

Pushing image 172.30.1.1:5000/scm-web-hooks-joris/scm-web-hooks:latest ...
Pushed 0/10 layers, 7% complete
Pushed 1/10 layers, 19% complete
Pushed 2/10 layers, 25% complete
Pushed 3/10 layers, 32% complete
Pushed 4/10 layers, 41% complete
Pushed 5/10 layers, 53% complete
Pushed 6/10 layers, 63% complete
Pushed 7/10 layers, 81% complete
Pushed 8/10 layers, 84% complete
Pushed 9/10 layers, 99% complete
Pushed 10/10 layers, 100% complete
Push successful
```

Now we are going to create a route for the application.

```
oc get service

NAME            CLUSTER-IP    EXTERNAL-IP   PORT(S)             AGE
scm-web-hooks   172.30.70.2   <none>        8080/TCP,8443/TCP   3m
```

Create the actual route.

```
oc expose service scm-web-hooks
```

Now test the application.

```
oc get route
```

Past the `HOST/PORT` section in your browser. This will get you to your deployment.

## Task 4 : Configure the github webhook

After we did the following steps we have created an application with one replica
running inside a docker container in Openshift.

* Navigate to the OpenShift Web console and login.
* Select your `Test WebHooks` project, and click `Builds` and then
`Builds`.
* Click onto the build name from the list. You should have just one in
this case.
* Click `Configuration` tab to get list of `Triggers` for the GitHub
link.
* Copy the `GitHub webhook URL`. You will need this URL for next step.

> INSERT SCREENSHOT

* Login to your GitHub account.
* Navigate to the forked repository you used to create the application.
* Click on Settings.
* Click on Webhooks.
* Click on the `Add webhook` button.
* Add the recently copied Web Hook URL from OpenShift.
* Change the Content-type as `application/json`
* Click on the `Disable SSL Verification` button.
* Confirm by adding the `Add Webhook` button in green at the bottom of
the page.

> INSERT SCREENSHOT

* Edit in your GitHub account the `image.php` file.
* There are a number of things you could change, but we are going to change the
color to a static color. Remove the following lines and add the new line.

To delete :

```
if ( $deployment == 'blue') {
  $color = imagecolorallocate($im, 0, 255, 0);
} elseif ($deployment == 'green')  {
  $color = imagecolorallocate($im, 0, 255, 0);
} else {
  $color = imagecolorallocate($im, 0, 0, 255);
}
```

To add :

```
$color = imagecolorallocate($im, 0,255,0);
```

This will staticly use the green color. 

* Commit the file.

* After saving/committing the `image.php` file with the small change,
you’ll notice in the OpenShift Web Console that a new build process has
been automatically triggered. `You didn’t have to start a build
yourself.`
* Monitor the build process using:

```
oc get builds

oc logs build/the-new-build-process-name
```

Don't delete your deployment, we are going to use this for the next lab.
