# What RESTful actually means

If you do web development, you’ve probably heard of REST. But if you’re like me, you usually just pretend to know what it is, and nod politely when someone asks you if what you’re making is RESTful. I use HTTP, err, that means it’s RESTful right? Recently, I decided to take the plunge and actually find out what this peaceful-sounding buzzword means.

# What is REST?

REST stands for Representational State Transfer. It is a set of design principles for making network communication more scalable and flexible. These principles answer a number of questions. What are the components of the system? How should they communicate with each other? How do we ensure we can swap out different parts of the system at any time? How can the system be scaled up to serve billions of users?

Roy T. Fielding first coined the term REST in 2000, in his PhD dissertation [Architectural Styles and the Design of Network-based Software Architectures](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm). At the time of the dissertation’s publication, the World Wide Web (or “the Web” for short) was already very popular. Fielding essentially took a step back and analyzed the traits that made the Web more successful than competing Internet protocols. He then envisioned a design framework for making network communication “web-like.” So REST is a generic set of principles not specific to the Web. It can be applied to other kinds of networks such as embedded systems. REST is also not a protocol since it does not prescribe implementation details.