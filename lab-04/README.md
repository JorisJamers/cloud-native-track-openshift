# Lab - 04 Using templates

> NOTE: Guide is not really the same on minishift, needs a good refactor. 

## Task 1 : Create a Project

Login to the web console in case you are not logged in anymore. If you want you
can use a project that you have already created, otherwise create a new one.

You can use the button `Create Project` and call it `templateproject-username`.
The `Display Name` and `Description` are yours to choose. This doesn't really
matter.

Press `Create`. You can get the same result from the following command in `CLI`

```
oc new-project templateproject-username
```

## Task 2 : Create a MYSQL database using the template

Click on `Add to Project -> Browse Catolog` button and you will be taken to select an
image or template. You will see the application create screen as shown
below:

![service_catalog2](../images/service_catalog2.png "service_catalog2")

Click on `Databases` tab. Find `MySQL` then `MySQL (Ephemeral)`
template from the list and click `Select`. You will also notice `MySQL
(Persistent)` template. But we will address that in a different lab
exercise.

You will be taken to the mysql ephemeral creation screen. Click `Next`
parameters and edit the values to use the following values:

```
Add to Project: consoleproject-UserName
Database Service Name: mysql
MySQL Connection Username: pricelist
MySQL Connection Password: pricelist
MySQL root user Password: pricelist
MySQL Database Name: pricelist
```

Click `Create`.





## Task 3 : Add a PHP frontend to talk to the database

## Task 4 :
