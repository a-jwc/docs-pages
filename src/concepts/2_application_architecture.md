# 02. Application Architecture

<div class="coreconcepts-intro" markdown=1>
Applications built with Holochain are highly **modular**. This makes it easy to share code and [compose](https://en.wikipedia.org/wiki/Composability) smaller pieces together into larger wholes. Each functional part of a Holochain application, called a **DNA**, has its own set of rules, private network, and distributed database.
</div>

<div class="coreconcepts-orientation" markdown=1>
### <i class="fas fa-thunderstorm"></i> What you'll learn

1. [Agent-centric integrity: inside, outside, and in between](#agent-centric-integrity-inside-outside-and-in-between)
2. [Layers of the application stack](#layers-of-the-application-stack)

### <i class="far fa-atom"></i> Why it matters

A good understanding of the components of the tech stack will equip you to architect a well-structured, maintainable application. Because Holochain is probably different from what you're used to, it's good to shift your thinking early.
</div>

## Agent-centric integrity: inside, outside, and in between

Before we talk about the tech stack, let's talk about donuts. That's a good way to start, isn't it?

![](https://i.imgur.com/7pj8fBx.png)

This is Holochain. Thanks to the magic of gluten, it has enough integrity to hold itself together. It separates the universe into two empty spaces---the hole and the space beyond.

![](https://i.imgur.com/nNuA1CZ.png)

On top of Holochain is your application. Each application has a different flavor.

![](https://i.imgur.com/ImkR73e.png)

Let's put you inside the hole. You have agency---the power to receive information from your world and act on it. Together, your copy of the Holochain runtime and your application mediate between you and Holochain land. Your application defines a set of functions that define all the valid ways you can interact with it, and Holochain exposes those functions to you.

![](https://i.imgur.com/Nvn4HIa.png)

On the outside of the ring is a shared space; in it are the other people using the same application. Holochain mediates interactions with them too, shuttling information across space with the help of a computer network. Again, your app defines what it considers valid, on this side through a set of rules that define what data should look like.

Holochain creates a 'double membrane' for each participant, bridging between their world and the digital space they share with others. It ensures the integrity of information passing through both the inside and the outside. This lets people safely do the things that are important to them, without having to depend on a central authority.

## Layers of the application stack

Now, let's get into the details of how a Holochain app is put together. Holochain apps (**hApps**) are made from loosely coupled components. Here's how they are built:

<div class="coreconcepts-storysequence" markdown=1>
1. ![](https://i.imgur.com/VVAX0Jc.png)
Code modules called **zomes** (short for chromosomes) define the core logic of your app. They contain functions to initialize a user's account; store, validate, and retrieve data; and respond to messages from other users. You can expose some of these functions as the zome's API.

2. ![](https://i.imgur.com/RMnObHc.png)
One or more zomes are combined into a **DNA** that defines the basic functionality and 'rules of the game' for a portion of an application's functionality. You can think of it like a [microservice](https://en.wikipedia.org/wiki/Microservices). The running DNA instance is the user's personal **agent**---every piece of data that it creates or message it sends, it does so from the perspective of the user.

3. ![](https://i.imgur.com/ogtDACY.png)
A user's DNA instances can talk to each other's APIs via **bridging**. This lets you compose them into a bundle of functionality that's needed for a full-featured app.

4. ![](https://i.imgur.com/d2aADQt.png)
A **client** on the user's device, such as a GUI or utility script, talks to the DNAs' APIs via a lightweight [remote procedure call (RPC)](https://en.wikipedia.org/wiki/Remote_procedure_call) interface. The client is like the front end of a traditional app and can be written with whatever language, toolkit, or framework you like. This client and its DNAs make up a **hApp bundle**.

5. ![](https://i.imgur.com/2TEFXbQ.png)
All DNAs are hosted in the user's **conductor**, a runtime that sandboxes and executes DNA code, manages data flow and storage, and handles connections between components of the stack. You can think of the conductor as a web application server.

6. ![](https://i.imgur.com/FSKeHnJ.png)
Each conductor is a **node** in a peer-to-peer network of agents using the same app. Each DNA in the hApp has its own separate private network and distributed data store. The conductor handles communication and data sharing between nodes.
</div>

Functional components and architectural layers both enjoy clean separation. You can combine, augment, or replace existing pieces. This gives you a lot of flexibility and empowers your users to take ownership of their experience.

!!! info
    All functions in your DNA start with a fresh memory state which is cleared once the function is finished. The only place that persistent state is kept is in the user's device storage. If you've written applications with REST-friendly stacks like Django and PHP-FastCGI, or with [function-as-a-service](https://en.wikipedia.org/wiki/Function_as_a_service) platforms like AWS Lambda, you're probably familiar with this pattern.

## Key takeaways

You can see that Holochain is different from typical application stacks. Here's a summary:

* Each user has their own copy of the application's front end (client), back end (DNAs), and server (conductor).
* The conductor sandboxes the DNA code, mediating all access to the device's resources, including networking and storage.
* All code is executed on behalf, and from the perspective, of the individual user.
* Users communicate and share data directly with one another rather than through a central server or blockchain validator network.
* Holochain is opinionated about data---it handles all storage and retrieval. (We'll learn about why and how in the next three articles.)
* DNA functions don't maintain any in-memory state between calls.
* Persistence logic and core business logic are mixed together in your DNA, because at its heart, Holochain is a framework for data validation. However, you usually don't need much code in your DNA---just enough to encode the 'rules of the game'.
* As with microservices, Holochain lends itself to combining small, reusable components into large applications.

## Learn more

* [Building Holochain apps: DNA](../../guide/building_apps)
* [Building Holochain apps: zome code](../../guide/zome/welcome)
* [Building Holochain apps: user interfaces](../../guide/apps_user_interfaces)
* [Building Holochain apps: bridging](../../guide/bridging)
* [Running Holochain apps: conductors](../../guide/conductors)
* [Holochain: Reinventing Applications](https://medium.com/holochain/holochain-reinventing-applications-d2ac1e4f25ef)
* [The Holo vision: Serverless 2.0](https://medium.com/holochain/the-holo-vision-serverless-2-0-c0b294e753ba)

## Tutorials

<div class="h-tile-container">
    <div class="h-tile tile-alt tile-tutorials">
        <a href="../../tutorials/coreconcepts/hello_holo">
            <h4>01: Hello Holo Tutorial</h4>
        </a>
    </div>
    <div class="h-tile tile-alt tile-tutorials">
        <a href="../../tutorials/coreconcepts/hello_test">
            <h4>02: Hello Test Tutorial</h4>
        </a>
    </div>
</div>
