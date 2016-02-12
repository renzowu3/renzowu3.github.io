---
layout: post
title: Single Sign On Tutorial
permalink: /sso/
---

----------
Single sign on is a user authentication process that permits a user to enter one username and password in order to access multiple applications.

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
 4. Upload the second web application `SSO-APP2.war` to your Bluemix account.
  > `cf push APP2-<your_name> -m 256M -p SSO-APP2.war`

	**Example:**
 >`cf push APP2-renzo -m 256M -p SSO-APP2.war`
 5. The web applications you deployed will be available in the `Applications` section in your `Dashboard`.

----------

 **Add and Configure Single Sign On Service**
 








