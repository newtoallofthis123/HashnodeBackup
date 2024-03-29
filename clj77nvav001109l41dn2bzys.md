---
title: "Abstraction and Cloud Computing"
datePublished: Wed Jun 21 2023 14:00:01 GMT+0000 (Coordinated Universal Time)
cuid: clj77nvav001109l41dn2bzys
slug: abstraction-and-cloud-computing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687442384607/c8663312-2c71-4d74-83dd-cd0d672b4c71.jpeg
tags: cloud, docker, opinion-pieces

---

I am currently running my site on [vercel](https://vercel.com/). An excellent saas that makes it easier for developers to deploy their applications and ship them faster without worrying too much about servers, CDN and concurrent users. I have been using it for a while now and I am very happy with it. However, it was not until a while back when I started to learn docker and get into the world of DevOps, that I realized how much I was taking for granted.

Platforms like Vercel, Netlify, Heroku, etc. are the modern standard for deployment, with many startups choosing to let them handle all of the nitty gritty, focusing on the product instead. These platforms provide excellent abstraction, sometimes to a point where all I have to do to deploy changes to my application is to just click 2-3 buttons on GitHub Desktop and their web interface. Now I always had this privilege, but I never really appreciated it until I started to learn about docker and DevOps.

To be honest, it is quite complex, setting up a *production-ready* server, with all the bells and whistles. Then choose the perfect base image for your application and configure various stuff like environment variables, reverser proxies and whatnot. It is a lot of work, and I am not even talking about the security aspect of it. This sort of abstraction is what makes it possible for developers to focus on the product and not worry about the infrastructure. It is a great thing, but it is also a sort of bad thing at the same time.

Now don’t get me wrong. Abstraction is a great thing, and it is what makes it possible for us to build complex systems. I mean, I don’t want to write the complex logic of a database, I just want to use it. If you use Python and like CLI you might have heard about a Python package called [rich](https://rich.readthedocs.io/en/stable/introduction.html) that is an abstraction for making CLI’s. It is a great package, and it makes it possible for developers to make beautiful CLIs without having to worry about the underlying systems. So, you don’t need to calculate the user terminal size, or worry about the color codes, worry about the cursor position, etc. You just use the package and it does all of that for you. So, abstraction is needed to sort of make it easier for developers to build applications. However, it is not without its flaws.

Now it seems hypocritical of me to even write this considering I started my programming journey in Python and still mostly code in higher-level languages. However, recently I realized the importance of understanding the underlying systems, mostly because of learning rust 😄. I am increasingly gaining interest in the low-level stuff. Hence, here I will be talking about how abstraction has changed the way we build applications, and how it has changed the way we think about applications. However, first, we have to look at the history of computing and how we got to where we are today.

## **Emergence of Cloud Computing**

Before the advent of serverless, developers had to manage their own servers. They had to worry about the hardware, the operating system, the network, the security, etc. This was a lot of work, and it was not very efficient.

> *“It works on my machine” - Every developer ever*

Now the problem with this approach is that it is not very scalable. You can’t just have a bunch of developers managing their own servers. It is not efficient, and it is not scalable. This is where the concept of *cloud computing* comes in. The concept was quite simple actually. Instead of having a bunch of developers manage their own servers, you manage a bunch of servers and charge developers for using them. This was sort of the start of Amazon Web Services. AWS was one of the first to win this race. They started with a simple service called EC2, which allowed developers to rent virtual machines. Now, AWS is so big, there are whole services and open-source tools that just help you manage your AWS infrastructure. It is crazy. I personally have not used AWS, but I have heard a lot about it. I have used the Google Cloud Platform, and it is quite similar to AWS. With that being said, I am not going to talk about AWS or GCP, but rather about the concept of cloud computing.

So, with the emergence of this new concept, we saw the emergence of a whole new paradigm of computing. This was the start of the *as a service* era. You had *infrastructure as a service*, *platform as a service*, *software as a service*, etc. Nowadays you even have Backend as a Service, with the emergence of services like Firebase, and Supabase.

Even newer ways of building applications also started to emerge. You had the JAM stack, which stands for JavaScript, APIs and Markup. So, in this approach, you have a static site, which is hosted on a CDN, and then you have a bunch of APIs that you can call to get data. This made the site a lot faster, and it was also a lot easier to manage. You could just use a static site generator like Gatsby or Next.js and then deploy it on a CDN. For the backend, you can use a bunch of reverse proxies like Nginx, Traefik, etc. to route the requests to the correct API. This was a great approach, and it is still used a lot. However, it is not without its flaws. The biggest problem with this approach is that it is not very secure. You have to expose your API to the public, which is not a good idea. This is where serverless came in with a bang.

## **Serverless**

Serverless is a concept that has been around for a while now. It is not a new concept, but it has gained a lot of traction in recent years. The idea is quite simple. Instead of having a server that is always running, you have a server that is only running when it is needed. So, if you have a function that is called once a day, you don’t need to have a server running 24/7. You can just have a server that is only running when the function is called. Now this is like the textbook definition of serverless, let’s look into what that actually means.

Take this site for example, which uses Astro and Vercel. Now, I don’t have a server running 24/7. I just have a bunch of static files that are hosted on a CDN. However, I have a bunch of what vercel calls *serverless functions*. These are just functions that are called when a request is made to a specific endpoint. The endpoints can vary from framework to framework, but the concept is the same. I normally use these functions to fetch data from my database, or to send emails, etc. This is a great approach, and it is a lot more secure than the JAM stack approach. This is because the functions are not exposed to the public. They are only called when a request is made to a specific endpoint. You have complete control over what endpoints are exposed to the public, and what endpoints are not.

This is a great approach when building small to medium-sized applications. However, it is not without its flaws. The biggest problem with this approach is that it is not very scalable. I mean, you can’t just have a bunch of functions that are called once a day. You need to have a bunch of functions that are called every second. This is not the most cost-effective approach.

You need actual servers to handle that sort of load.

## **Containers and Docker**

Now, this is where containers come in. Containers are a way to package your application and all of its dependencies into a single package. It is sort of like a virtual machine, but it is a lot more lightweight. So it still runs a very small operating system and has a hypervisor and all that stuff. However, it does not have a kernel. It uses the kernel of the host machine. This makes it a lot more lightweight than a virtual machine. Now, you can have a bunch of containers running on a single machine, and they will all be isolated from each other. So, as you probably might have guessed from the symbol of docker, it is a containerization tool. It is a tool that allows you to create and manage containers.

Docker also made it a lot easier to create and manage containers. It also made it a lot easier to share containers. This is because docker introduced the concept of *images*. An image is just a snapshot of a container. You can use this image to create a container. Now, you can share this image with other people, and they can use it to create a container. Hence you made a constant system of collaboration. This is what made docker so popular.

The way it fits into the whole cloud computing paradigm is that you can use docker to create a container that has your application and all of its dependencies. You can then use this container to run your application on a server. This is a great approach, and it is a lot more scalable than serverless. You can control the RAM and system resources that are allocated to the container, and you can also control the number of containers that are running. Hence you can handle concurrent requests a lot better. This is a great approach, and it is a lot more scalable than serverless.

## **The Problem**

So, all this is very wonderful. When I built my first application, I had used a simple flask server that was running on a single machine. I then had used [Heroku](https://www.heroku.com/) to deploy it. It was a great experience, and I learned a lot. The thing was, I knew nothing about what I was doing. I just followed a tutorial and got it working. I had no idea what was going on behind the scenes. I for the longest time had no idea what exactly Heroku even was. I just knew that it was a service that allowed me to deploy my application. I had no idea what a dyno was, or what a slug was. I just knew that I had to push my code to a git repository and it would get deployed.

Now you might say this is a good thing. I mean, I was able to deploy my application without knowing anything about what was going on behind the scenes. This would be a god sent for a lot of people. I would however argue that this approach would not work for a lot of people. Imagine if you were a developer who was working on a large-scale application. You would need to know what was going on behind the scenes. You would need to know exactly why and what is being allocated to your application. Imagine you are paying actual money for this, you would be obligated to understand the whole thing, to make sure that you are not wasting your money.

This is where I think the problem lies. I think that the whole cloud computing paradigm is too complicated. I think that it is too complicated for the average developer. That is the reason all these abstraction layers exist. That is the reason why you have all these services that just help you manage your AWS infrastructure. Now I am not saying that these services are bad. I am just saying that they are not for everyone.

For my site, I use Vercel. I use it because it is simple. I don’t have to worry about anything. I just push my code to a git repository and it gets deployed. Every once in a while, a deployment fails, I fix a few things and it works. I also use MongoDB Atlas for my database. I write simple queries and it works.

However, if I had to write a, let’s say a bank application, I would not use Vercel. I would not use MongoDB Atlas. I would not use any of these services. I would want to have complete control over my infrastructure. I would want to know exactly what is going on behind the scenes. Now take this with a grain of salt, this is just my opinion. I am not saying that you should not use these services, but I am saying that you should know what is going on behind the scenes.

## **Costs and Security**

This in itself deserves an article of its own, so I am not going to go into too much detail. I am just going to give you a brief overview of what I think. Most platforms like Vercel and Netlify have a free tier. This is great, and it is a great way to get started. However, once you start getting a lot of traffic, you will have to upgrade to a paid plan. So, essentially, you are paying relative to the amount of traffic that you are getting. This is great if you are a small company with a few million requests a month. That would probably cost you around 100$ a month. However, if you are a large company with a few billion requests a month, that would exponentially increase your costs. So, the whole paradigm of paying relative to the amount of traffic that you are getting is not very scalable. Let’s say you coded your whole infrastructure to fit the serverless paradigm. You have a bunch of functions that are running on a serverless platform. What then happens when your company finally decides to move away from the serverless paradigm? What then happens when you have to move to a more traditional approach? You might have to rewrite your whole infrastructure. Just saying, that’s a lot more costlier than you might think.

What about the other approach then? Even when you are a small company, you are spending thousands of dollars a month on your infrastructure. Most of which you might be bearly using. What happens then when if your startup fails? What happens then if you have to shut down your company? You would have spent thousands of dollars on your infrastructure, and you would have to shut it down. That is a lot of money down the drain.

It’s a weird situation. If you try and make the process way too easy, you open yourself up to a lot of problems, if you don’t good luck waking up one day and finding out that you have been paying for a bunch of servers that you don’t need.

## **The Solution**

Like most topics I discuss, I don’t have a solution. I just have a bunch of ideas. I think that the whole cloud computing paradigm is way too complicated in its current state. As I said, if you try and make the process way too easy, you open yourself up to a lot of problems, if you don’t good luck waking up one day and finding out that you have been paying for a bunch of servers that you don’t need. Having an AWS bill of 1000$ is not the best way to start your day.

We are also recently seeing many companies moving away from the whole microservices and serverless approach. We are seeing companies like Amazon Prime moving back to a more traditional approach. Having huge monolithic applications that are running on a single server. This is a great approach, and it is a lot more cost-effective than the whole microservices approach. However, once again, do you really need to have a server running 24/7?

One more thing that is quite frequently overlooked is the environmental impact of all this. I mean, we are running a bunch of servers 24/7. This is not very good for the environment. Serverless on the other hand is a lot more environmentally friendly. This is because you only have a server running when it is needed. You know that thing that used to happen on heroku free tier, where your application would go to sleep after 30 minutes of inactivity. That was a great approach.

Once again, my dear reader, I leave you there, with a bunch of questions. I hope that you enjoyed this article. I hope that you learned something from it. I know I did writing this. I hope that you have a great day, and I will see you in the next one. Till then, say that to my `/api` endpoint.