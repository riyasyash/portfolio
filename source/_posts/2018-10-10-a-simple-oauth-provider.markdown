---
layout: post
title: "A Simple OAuth Provider"
description: "Recently, I had to implement an OAuth Provider for one of my projects (So that people can log in to a different application using their credentials on my app), which was using JWT token-based authentication."
date: 2018-10-07 00:00:00
comments: true
image: https://cdn-images-1.medium.com/max/1600/1*qatotphqCyOKDuGbDl4Qwg.jpeg
keywords: "oauth, python, django-rest-framework, django"
category: tech
tags:
- tech
---
Recently, I had to implement an OAuth Provider for one of my projects (So that people can log in to a different application using their credentials on my app), which was using JWT token-based authentication. So I read through a lot of documentation and implementation models. Fortunately, since we were using django-rest-framework I could find a lot of good writeups. This is one among them Oauthlib.

After reading the particular writeup, I decided to implement the provider our selves (since it seemed pretty simple, 😅and it turned out simple too!)

Here, we will be implementing OAuth through Authorization Code (Yeah, there are other methods as well.) The code will be more Django specific, but you can make use of the concepts and the models to implement the same in any other languages of your choice.

## How is it working?
<br>

<!-- {% include image.html url="https://cdn-images-1.medium.com/max/1600/1*HcZ1gZ_7SbeY6V5h6N13Pw.jpeg" description="diagram depicting the authentication flow" %} -->
<figure class="image"><center>
    <img src="https://cdn-images-1.medium.com/max/1600/1*HcZ1gZ_7SbeY6V5h6N13Pw.jpeg" alt="{{ diagram depicting the authentication flow}}">
    <figcaption>{{ "diagram depicting the authentication flow" }}</figcaption>
</center>
  </figure>
<br>

1. The third party app (the application to which the user has to login) redirects to our authorization page with the client_id, that they get at the time of registration and optional success and error redirect URIs.<br><br>
2. Our authorization page will validate whether a user is currently logged in or not (by checking the cookies). If there is a logged in user the page will ask the user for authorizing the access, if not the page will ask to log in with credentials. After that, the page requests our application backend to generate an authorization code for the client for the logged in user.<br><br>
3. Our application backend ensures client and user validity and generates an authorization_code which expires in 10 minutes and responds with the code and redirect_uri (if any was registered with the client).<br><br>
4. The authorization page redirects to the redirect_uri obtained from the application backend (or the success URI passed as the query parameter) with the authorization code.<br><br>
5. The third party app requests our application backend to generate a user token with the obtained authorization_code, client_id, and client_secret obtained at the time of client registration.<br><br>
6. The application backend validates the credentials and authorization code and generates a user token for the third party app.

## Let’s Begin

We need to write the CRUD APIs to register a client, update details for a client and delete a client (I will not be covering them here🤓).

We need two models to store the OAuth related data

1. Client: Which will store the details of the third party application which has to access our app’s data.
2. Authorization Code: Which will store the authorization_code, the user and client details for whom the code was generated and the expiry time of the particular authorization_code.

We need to write functions to perform the following operations

1. To generate an authorization code after validating the client.
2. To generate the actual user token after validating the authorization code and client credentials
3. Optional function to invalidate the authorization code after generating the user token

## Let’s Look at the code

{% gist 32180f78111b8cda15843a9b9094b560 %}

The functions generate_client_secret() and generate_token() can be any method that generates a random string with a length satisfying OAuth specification. The function_to_generate_token() has to be replaced with whatever you are using to generate user tokens (in my case it is JWT).

## That’s it!

Now you know how an OAuth provider can be implemented!.
