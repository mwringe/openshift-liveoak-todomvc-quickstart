#LiveOak ToDoMVC Example QuickStart

This OpenShift QuickStart will create and configure a DIY gear to host the LiveOak ToDoMVC example's HTML 5 client side code. It will requires access to a LiveOak instance already configured for the ToDoMVC example's backend.

For more information on how to configure a LiveOak gear in OpenShift with the example's backend already configured, please refer to the following quickstart:

https://github.com/liveoak-io/openshift-liveoak-examples-quickstart

Or refer it its application.json file available [here] (TODO: insert link here)

To ToDoMVC example showcases some of the security features of LiveOak. TODO: add a bit more detail here.

If you wish to run the ToDoMVC example locally on your own machine, please see the  example available here:

https://github.com/liveoak-io/liveoak-examples/tree/master/todomvc

#Installing the ToDoMVC Client Example

To install the quick start from the 'rhc' tool:

```
rhc app create mytodolist diy --from-code git://github.com/liveoak/openshift-liveoak-client-todomvc-quickstart
```

or install from the OpenShift console using the DIY cartridge with the source code option set to git://github.com/liveoak/openshift-liveoak-client-todomvc-quickstart 

This example assumes that you have your LiveOak instance running on a gear under your same account called 'liveoak'. If you have your liveoak instance running on another machine, please edit the diy/js/app.js.erb file to modify the host and or port to point to the LiveOak instance you want to use.

For example, if your LiveOak is running on a site called 'myAwesomeMBaaS.com' on port 80, you would modify the following line in diy/js/app.js.erb from

```
host: "liveoak-<%= ENV['OPENSHIFT_NAMESPACE'] %>.<%= ENV['OPENSHIFT_CLOUD_DOMAIN'] %>",
port: 80,
```

to

```
host: "myAwesomeMBaaS",
port: 80,
```

This example assumes that you have already configured your LiveOak instance for the 'todomvc' example. 

The easiest way to do so is to install the LiveOak example quickstart which can be found here: https://github.com/liveoak-io/openshift-liveoak-examples-quickstart

#Configuring the ToDoMVC Client Example

The following steps assume that your liveoak instance is running on a gear in OpenShift with a url like http://liveoak-USERNAME.rhcloud.com, you will need to adapt the urls listed to your own specific environment.

The following steps also assume that your todo gear is available at a url like http://todo-USERNAME.rhcloud.com, you will need to adapt the urls listed to your own specific environment.

A few more steps will need to be completed before you can run the ToDoMVC example. This includes setting up a MongoDB collection for the example, and authorizing your gear for use in LiveOak.

1. Creating a MongoDB collection for the example.
  * login to the admin console at http://liveoak-USERNAME.rhcloud.com/admin#/applications/todomvc/storage/storage/browse
  * click on 'New Collection' and call this collection 'todos'

2. Create roles for your application (Manual step required)
  * login to the admin console at http://liveoak-USERNAME.rhcloud.com/admin#/applications/todomvc/application-settings
  * add 2 new roles "admin" and "user". 
  * select "user" to be default role 
  * click "Save"

3. Add an HTML client for your ToDOMVC Gear
  * login to the admin console at http://liveoak-USERNAME.rhcloud.com/admin#/applications/todomvc/application-clients
  * click 'add client' and fill in the following values:
    * Name: "todomvc-html-client"
    * Platform: HTML-5
    * Redirect URI: "http://todomvc-USERNAME.rhcloud.com/*" (click button "Add")
    * Web Origins: "http://todomvc-rhmwringe.rhcloud.com" (click button "Add")
    * Scope: select both "admin" and "user" scopes
  * click 'save'

#Accessing the ToDoMVC Client

After you your gear has been created, you should be presented with a link to access the website. Accessing the website will take you to the ToDoMVC example, which allows you to configure a ToDo list.

The first time you access this page it may ask you to login as a user. To create a new user, please click on the 'register' link. Alternatively, you can also manage your users through the KeyCloak admin console, which is available at http://liveoak-USERNAME.rhcloud.com/auth/admin
