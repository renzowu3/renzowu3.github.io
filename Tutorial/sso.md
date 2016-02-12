---
layout: post
title: Single Sign On Tutorial
permalink: /sso/
---
----------
Single sign on is an user authentication process that permits a user to enter one username and password in order to access multiple applications.

In this tutorial you will learn how to use single sign on for user authentication. In order to see the difference between applications with and with out single sign on, you will first try to log in to multiple applications with out single sign on service.

----------

**Download the Web Applications**


You will download two web applications that will be deploy in your Bluemix account.

 1. Create the directory `SSOtemp` in the root directory. Create two subdirectory `Application1` and `Application2` in `SSOtemp`.
 
 2. Download SSO-APP1.war and SSO-APP2.war and save them to `Application1` and `Application2` subdirectory respectively.

----------
**Deploy the web applications in Bluemix using `cf` tool.**

 1. Open a terminal window and go to the `Application1` subdirectory.
 2. Login to your Bluemix account using the `cf` tool. It will ask your username (e-mail address) and password.
	 >  `cf login -a  https://api.ng.bluemix.net -s dev`
	 
 3. Upload the first web application `SSO-APP1.war` to your Bluemix account.
 > `cf push APP1-<your_name> -m 256M -p SSO-APP1.war`

	**Example:**
 >`cf push APP1-renzo -m 256M -p SSO-APP1.war`
 4. Go to the `Application2` subdirectory.
 
 5. Upload the second web application `SSO-APP2.war` to your Bluemix account.
  > `cf push APP2-<your_name> -m 256M -p SSO-APP2.war`

	**Example:**
 >`cf push APP2-renzo -m 256M -p SSO-APP2.war`
 5. The web applications you deployed will be available in the `Applications` section in your `Dashboard`.

----------

 **Create Single Sign On Service**
 
 

 1. Go back to the browser containing your Bluemix account. In the menu bar, click `Catalog`.

 2. Search for the `Single Sign On` service and click it.
 
 3. In the `Service name` text box, enter any name you want.
 
 4. Click `Create`.

 5. You will be ask to type a `unique ID` for the service.
 
	 **Note:** 
	 The name that you are prompted for in this step is not the same as the name displayed in step 5. This name is a unique ID that becomes the URL prefix for the redirect URL of your service. The name can be up to 32 characters in length and must start with an alphanumeric character. You cannot change this name unless you delete and then re-create the service.

 6. Click `Continue`.
 
 7. As you can see on the left menu , you can add new `Identity Source` or add  existing ones which are `SAML Enterprise`, `Cloud Directory`, and `Social Identity Source`.
 
**Adding a Cloud Directory Identity Source** 

The `Cloud Directory` identity source uses a user registry that is hosted in the Cloud. It hosts password policies and user information.

 1. Click `Cloud Directory`.

 2. Type a name for the identity source and click save.
 
 3. Add a user to the directory. Click the `+` to add a user . Once you add a user you can `delete` or `edit` it.
 4. Click save. It is enabled by default.
 
 5. Click the Identity source you created.

 6. Click the `Settings` icon beside save button. Leave auto consent `on`.
> **Note:** Auto Consent setting is on, an application can retrieve the user's identity information without asking the user for consent. Turn off this setting to prompt the user before retrieving identity information.

 7. Click Password Policy. Explore different policy level.
 8. Click save. 

----------
**Bind Single Sign On Service to Web Applications** 

You will bind the service to the two web applications.

 1. Click `APP1-<your_name>` in your `Dashboard`.
 
 2. Click `Bind a Service or API`. 
 
 3. Choose the `single sign on service` you created and click `Add`. 

 4. Click `Restage`.
 
 5. Repeat step number 1 to number 3 for `APP2-<your_name>` 
 
 **Note:** Choose the `same single sign on service`.

 ----------
 **Integrating the Web Applications with the Service**

1.	 Go back to the `Dashboard` and click `APP1-<your_name>`.

2.	On the left menu, click `Single Sign On`.

3.	Click the `Integrate` tab to configure the application.

4.	Click Save.

5.	Repeat step number 1  to number 4 for `APP2-<your_name>`.

  ----------
 **Understanding How the Web Applications are configured** 

Set security constraints in `web.xml`.

    <security-constraint>
		<display-name><displayname></display-name>
		<web-resource-collection>
		  <web-resource-name><resourcename></web-resource-name>
		  <url-pattern>/</url-pattern>
		  <url-pattern>/*</url-pattern>
		  <url-pattern>/<applicationname>/*</url-pattern>
		  <http-method>GET</http-method>
		  <http-method>PUT</http-method>
		  <http-method>HEAD</http-method>
		  <http-method>TRACE</http-method>
		  <http-method>POST</http-method>
		  <http-method>DELETE</http-method>
		  <http-method>OPTIONS</http-method>
		</web-resource-collection>
		<auth-constraint>
		  <role-name><rolename></role-name>
		</auth-constraint>
	</security-constraint>

Enable the security constraints in `server.xml`.

    <application type="war" id="<applicationname>" name="<applicationname>" 
               location="${server.config.dir}/<path_to_.WAR_file from server directory>">
            <application-bnd>
                <security-role name="<rolename>">
                    <special-subject type="ALL_AUTHENTICATED_USERS"/>
                </security-role>
            </application-bnd>
        </application>

 ----------
**Launch the Application**

 ----------
 **End of Tutorial**
