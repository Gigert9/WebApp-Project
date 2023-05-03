# WebApp-Project

The first project completed during Georgia Tech's Cybersecurity and Networking Bootcamp involved creating and deploying a web application through a virtual environment built with Microsoft Azure. This was accomplished over three class days, however I commited several hours outside of class to adjusting and expanding the site through changes to the HTML and CSS files. 

This was an exceptionally fun project, and it was nice to have something to show after all the work we had put in thus far. Still the final version of the site (shown below), looked a bit too much like a school project to suit my vision. I'll address these concerns farther down...

# The Setup

In the previous classes, we created a virtual network that consisted of:
  - Security group acting as a firewall
  - Jump Box to act as an API gateway for the network administrator.
      - The jump box also acted as a point to use Ansible to configure and launch multiple docker containers across our web servers
  - Three web servers hosting a Damn Vulnerable Web Application via Apache from within a docker container
  - Load Balancer that directed outside HTTP traffic towards a back-end pool consisting of our three web servers

The following diagram outlines the virtual network that was established:

![TONY GASH Cloud Security](https://user-images.githubusercontent.com/101701044/235814044-dbe3247b-ba26-4e58-8f42-89567353761c.png)

# Making a WebApp

From this point, we then created a web application via Azure, that we then hosted within our virtual network. Using the Azure Cloud Shell, we then configured and deployed a Docker container that would host a template website from our web application. 

For comparison, I am including a photo of the original template we were given:

<img width="942" alt="project1_13b" src="https://user-images.githubusercontent.com/101701044/235816546-3d48bb2a-0bb4-435e-a291-7210198a611b.png">

In addition to configuring a container on our web application, we also had the option to purchase a domain name from GoDaddy to use. I chose to do so, purchased the domain "spaldingtech.com", and pointed it at the web application being hosted on Azure. 

We then created a key vault on Azure where we experimented with self-signed certificates before creating and using an app service managed certificate. This allowed us to restrict traffic to HTTPS only, as well as avoid trust issues with broswers attempting to connect to our site.

Finally, we created a front door instance through Azure and created custom WAF rules for our web application. 

A truncated image of the final version of my website:

![site](https://user-images.githubusercontent.com/101701044/235815824-5ff857f3-844a-4785-a6d0-4aecd84cec51.png)

# Moving Forward

After leaving the site running through Azure for several days I encountered a few issues. Primarily, the basic plan we had used in class did not offer enough instances of the site to guarantee it would be available for every connection attempted. Working on this site around others and asking them to visit, resulted in many people discovering the site would not load at all. When I told Azure to create additional instances, I discovered the Docker container we had used to establish the site would default back to the template everytime the web application was restarted. This also affected the instances that were created. 

My plan is to configure an old server I have to host the site myself. This would bypass both the restrictions of the Docker container provided by the class, as well as the cost of using Azure's services. In the meantime, I made use of the GoDaddy site builder to create a much more professional looking website.

