# What RESTful actually means

If you do web development, you’ve probably heard of REST. But if you’re like me, you usually just pretend to know what it is, and nod politely when someone asks you if what you’re making is RESTful. I use HTTP, err, that means it’s RESTful right? Recently, I decided to take the plunge and actually find out what this peaceful-sounding buzzword means.

# What is REST?

REST stands for Representational State Transfer. It is a set of design principles for making network communication more scalable and flexible. These principles answer a number of questions. What are the components of the system? How should they communicate with each other? How do we ensure we can swap out different parts of the system at any time? How can the system be scaled up to serve billions of users?

Roy T. Fielding first coined the term REST in 2000, in his PhD dissertation [Architectural Styles and the Design of Network-based Software Architectures](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm). At the time of the dissertation’s publication, the World Wide Web (or “the Web” for short) was already very popular. Fielding essentially took a step back and analyzed the traits that made the Web more successful than competing Internet protocols. He then envisioned a design framework for making network communication “web-like.” So REST is a generic set of principles not specific to the Web. It can be applied to other kinds of networks such as embedded systems. REST is also not a protocol since it does not prescribe implementation details.

# The Fielding Constraints

Fielding’s dissertation outlines a number of architectural constraints that a system must satisfy to be considered RESTful. Below, I’ll give a brief overview of each of these constraints and discuss how the Web satisfies them using its core technologies: HTTP, HTML, and URIs.1(If you’re unfamiliar with URI, just think “URL”. There is a distinction, but it is not important to our discussion.) Let’s take a look at the Fielding Constraints one by one.

## **Client-server**

The first Fielding Constraint specifies that the network must be made up of clients and servers. A server is a computer that has resources of interest, and a client is a computer that wants to interact with the resources stored on the server. When you browse the Internet, your computer is acting as a client and sends HTTP requests to a server in order to access and manipulate information. A RESTful system has to operate in the client-server model, even if a component sometimes acts like a client and sometimes acts like a server.

A non-RESTful alternative to client-server architecture is event-based integration architecture. In this model, each component continuously broadcasts events while listening for pertinent events from other components. There’s no one-to-one communication, only broadcasting and eavesdropping. REST requires one-to-one communication, so event-based integration architecture would not be RESTful.

## **Stateless**

Stateless does not mean that servers and clients do not have state, it simply means that they do not need to keep track of each other’s state. When a client is not interacting with the server, the server has no idea of its existence. The server also does not keep a record of past requests. Each request is treated as a standalone.

## **Uniform interface**

The “uniform interface” constraint ensures that there is a common language between servers and clients that allows each part to be swapped out or modified without breaking the entire system. This is achieved through 4 sub-constraints: identification of resources, manipulation of resources through representations, self-descriptive messages, and hypermedia.

## **Interface constraint 1: identification of resources**

The first sub-constraint of “uniform interface” affects the way that resources are identified. In REST terminology, a resource could be anything – an HTML document, an image, information about a particular user, etc. Each resource must be uniquely identified by a stable identifier. A “stable” identifier means that it does not change across interactions, and it does not change even when the state of the resource changes. If a resource does get moved to another identifier, the server should give the client a response indicating that the request was bad, and give it a link to the new location of the resource.

The Web uses URI to identify resources, and HTTP as its communication standard. To get a resource stored on a server, a client makes a HTTP GET request to the URI that identifies that resource. Every time you type an address into your browser, your browser makes a GET request to that URI. If it receives a 200 OK response and an HTML document back, then it renders the page in the window so that you can view it.

## **Interface constraint 2: manipulation of resources through representations**