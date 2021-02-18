---
title: "What really happens when you click on a link...?"
date: "2020-12-31"
---

Have you ever thought about what happens when you click on a link in the web browser and get taken to a new web page? It's something that I'd never really considered until I started learning to program earlier this year...it just kind-of happened. The internet would work it's magic and I got taken to my desired location without another thought. On the odd occasion when things went wrong and I was served up an error message, I would spend a while baffling at what `404` really meant, try furiously refreshing the page a few times and then give up, assuming there was an angry gremlin in the system that didn't want me to buy another pair of shoes even if they were 60% off and definitely not like that other pair I already owned. But since learning to code earlier this year and becoming what you might call _internet savvy_, I've learnt that the process is far more complex than I ever thought. And super awesome! So prepare yourselves for an exciting journey across time, space and acronyms as I take you behind the scenes to find out what really happens when we click on a link...

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/8n64mf9ba2qlf9l7n0fg.jpg)

## The Internet & the World Wide Web

Before we dive into the details let's stand back and look at the big picture for a moment. What is the **internet**? Is it the same as the **World Wide Web**? The answer is no! Although we often use the terms interchangeably, the internet and the World Wide Web are not the same. The internet is a very big network of computers (more accurately a network of networks) transferring lots and lots of data around the globe. The World Wide Web runs on top of the internet - it is a huge distributed application running on millions of servers world wide and it is accessed using a special program called a web browser. The fundamental building block of the web is a single page - a document containing content which contains links to other pages. These links (text or images you can click on and they take you to another page) are called hyperlinks and they form a huge web of interconnected pages. Text containing hyperlinks is so powerful that it got named hypertext - the language of the web. Web pages are the most common type of hypertext document today and these pages are retrieved and rendered by web browsers which allows us to read them. In order for pages to link to each other, each hypertext page needs a unique address and this is specified by a **Uniform Resource Locator (URL)**.

## URL, IP & DNS

The URL is an address that shows where a particular page can be found on the World Wide Web. It is constructed in the following way:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/z1c3rvyskih35jd2btow.PNG)

The URL allows access to a specific resource on a web server and as we can see from above it's often a domain name followed by the page name. However, in order for the web page to be retrieved, the URL needs to be translated into an **IP address**. Web browsers interact through IP (Internet Protocol) addresses which are unique identifiers - you could think of them as a numerical label assigned to each device connected to a computer network.

> A protocol is just a system of rules that define how data is exchanged within or between computers. Communications between devices require that the devices agree on the format of the data that is being exchanged. We're going to learn about lots of other protocols as we go on...

Every computer connected to a network gets an unique IP address which other machines use to find the device, just like a street address is used to find a particular house. An IP address format looks like this: `AAA.BBB.CCC.DDD`. It’s a sequence of numbers (all between 001 and 255) separated by full stops. The below IP address is one of Google's servers:

### `172.217.7.238`

You can use the IP address instead of the URL to get content from a website (have a go typing the above IP address into the browser - you should get Google's home page) but it would be impossible to remember the IP address of every website! That's why domain names were invented. These domain names are translated into machine IP addresses with a DNS lookup. **DNS** stands for **Domain Name System** and it is a huge database where the domain name is stored with its corresponding IP address - you could think of it as the phone book of the internet.

So the first thing that happens when you click on a link is the browser issues a DNS address lookup to a DNS or naming server. It takes a domain name as input and replies back with the matching computers IP address. If the naming server doesn't have the address in its database, it will pass the address further up the naming server food chain. If no naming server can find the IP address, the failure is passed back down to your browser. At this stage you'll probably see an error message which might look something like this:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/g1w0dqav0xedziutti68.PNG)

If the address _is_ found, the IP address is sent to your browser and once the browser receives the IP address it opens a connection with the web server at the IP address you want. It then asks the web server for a specific page and it does this using HTTP.

## HTTP

**HTTP (HyperText Transfer Protocol)** allows the fetching of resources (eg. web pages) and it is the foundation of any data exchange on the web. It is a client-server protocol which means requests are initiated by the client (the web browser) and communication between the client and the server is via requests and responses. In the most basic terms, the client sends a `GET` request to the other computer (the server) via a command such as `GET/thepageyouwant` and the server responds with the information:

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/4v1pygyc7mhr22189q8j.PNG)

This information is interpreted by the web browser and rendered to the screen. To go to another page, your computer simply sends another request and this goes on and on. The first documented version of HyperText Transfer Protocol only had one command - `GET`. Now there are many more types of requests used to manipulate data on the internet. Some of these include `POST`, `PUT` and `DELETE` - you can [read more about the different types of HTTP requests here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods). In later versions, HTTP also added status codes which prefixed any hypertext that was sent following a request. For example, status code `200` mean everything's okay, I've got the page and here it is! Status codes in the 400's are for client errors, eg. `404 page not found` which means the file or page that the browser is requesting wasn't found by the server.

To communicate over the network, internet protocol is followed. TCP/IP (Transmission Control Protocol / Internet Protocol) is the most common protocol but before we find out more about that we're going to learn how data is actually sent over the internet...

## ROUTING & PACKETS

As we discovered at the start, the internet is a huge network of networks which sends data to and from different computers. Just like there are different roads you could take to drive to a destination, there are often multiple paths to get data from one location to another. **Routing** is the process of selecting a path for traffic in a network or between or across multiple networks. With millions of computers online all exchanging data, bottlenecks can appear and disappear in milliseconds. **Network routers** are constantly trying to balance the load across the network to ensure speedy and reliable delivery. This is called **congestion control**. Messages are passed through several stops on the way to their destination a bit like the postal service. When you post a letter from London to Edinburgh it might pass through a number of cities / sorting offices on the way, depending on traffic, road closures or transport routes, before it reaches Edinburgh. The same is true when sending data over the internet. Using different routes makes communications more reliable and fault-tolerant as if there is a blockage on one route, the message can take another route.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/q4mil4riho790t9n1zh9.PNG)

This message switching technique, in which messages are sent in their entirety from source to destination one hop at a time, is called **message switching**. And the number of hops a message takes along its route is called the **hop count**. Keeping track of the hop count is useful as it can help identify routing problems. The hop count is stored with the message and updated along its journey. If messages have high hop counts, most likely something has gone awry in the routing. However, the downside to message switching is that messages are sometimes big which means that they clog up the network because the whole message has to be transmitted from one stop to the next before continuing on its way. This ties up the whole route so no other messages can get through until it's done. Other messages have to wait until the big file transfer is finished or take a less efficient route which is not ideal. The solution is **Packet Switching**.

Instead of sending the whole message all in one go, big messages are chopped up into many smaller pieces called packets and sent individually across the network. They may take different routes but they all end up at the correct destination as each packet contains a destination address (IP address) so the network routers know which computer to forward them to.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ehe87s9b4cqa60bfoe0d.PNG)

Packets are made up of a header and a payload. Data in the header is used by networking hardware to direct the packet to its destination and the payload is the actual data being sent. Once the packet has reached its destination the payload is extracted and used by application software. Chopping up data into small packets and passing these along flexible routes with spare capacity is so efficient and fault-tolerant it's what the whole internet runs on today. Internet packets have to conform to a certain standard called IP - for example, each packet needs an address and there are limits to the size and weight of packages. However, IP is very low level protocol and there isn't much more than a destination address in the packets header. This means that a packet can show up at a computer, but the computer may not know which application to give the data to (eg. Skype or Call of Duty). For this reason, more advanced protocols were developed to sit on top of IP - UDP and TCP.

## UDP

So we've seen that IP gets the packet to the right computer but it's UDP which gets it to the right program. **UDP (User Datagram Protocol)** has its own header which sits inside the data. Inside the UDP is some extra useful information - the port number. Each program on the computer will have a unique port so when a packet arrives to a computer, the operating system will look inside the UDP header and hand it to the right program. The UDP header also includes a **checksum** which allows the data to be verified for correctness. The checksum sits in the header and it is the sum of all the data in each packet which is calculated before the packet is sent. When the receiving computer gets the packet it repeats this process, adding up all the data. If that sum is the same as the checksum sent in the header then everything is good! But if the numbers don't match, the data must have got corrupted at some point in transit. UDP doesn't offer any ways to fix the data or request a new copy so typically the packets are just discarded. It also doesn't offer any mechanisms to know if packets are getting through to their destination successfully or not. If different packets from the same message take different routes through the network the packets may arrive at their destination out of order or some may not arrive at all. This is fine for applications that rely on high speeds of data transmission such as video chat or online video games - if some packets don't arrive the video goes a bit glitchy for a seconds but it's not the end of the world. But it can be a problem for other types of data transmission such as an email or web pages. If only half of your email arrives or only half a web page loads this would not be good. Luckily there are other protocols (I told you there were a lot!) which we can use to handle this...

## TCP

This is where **TCP (Transmission Control Protocol)** comes into things. Like UDP it rides inside the data payload of IP packets. For this reason, people refer to this combination of protocols as TCP/IP. Like UDP, TCP contains the port and checksum along with some other fancier features. TCP packets are given sequential numbers so they can be put into the correct order when they arrive at the receiving computer by the TCP implementation in your operating system. TCP requires that once a computer correctly receives a packet and the data passes the checksum that it sends back an acknowledgement (ACK) to the sending computer. If enough time passes and the sending computer doesn't receive an ACK, the sending computer will presume the packet has been lost and send it again. The packet may not have got lost - it may be the ACK that got lost or it might just be taking a long time to send - but that doesn't matter. The important thing is that the packet has been sent again. If a duplicate packet arrives the receiver has the sequence number so can discard any duplicates. TCP isn't limited to a back and forth conversation - it can send many packets at once and have many outstanding ACKS which increases bandwidth significantly as you aren't wasting time waiting for ACK's to return. The success rates of ACK's and the round trip time between sending and acknowledging can be used to infer network congestion. TCP uses this information to adjust how aggressively to send packets - a mechanism for congestion control. It can throttle it's transmission rate according to available bandwidth which is pretty cool! So you may be thinking why use UDP when you've got TCP? Well all the ACK packets doubles the number of messages on the network yet your not actually transmitting any more data. That overhead is sometimes not worth the improved robustness especially for time critical applications like video chat or online gaming.

So...after our slight detour into routing and packets, let get back to our hyperlink. We've clicked on our link and it's performed a DNS lookup to find the IP address. Once the browser receives the IP address it initiates a connection with the server at that address using a process called **TCP 3-Way Handshake**. The client computer sends a `SYN` (synchronize) message to see whether second computer (the server) is open for new connection or not. If the server is open for a new connection too it sends an `ACK` (acknowledgement) message with a `SYN` message as well. After this the first computer receives its message and acknowledges it by sending an `ACK` message back.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/eowtuw0ph7a707dtn2ev.PNG)

Now the connection is built between the client and the server they can both communicate and share information with each other. The browser can send a HTTP `GET` request to the server for a specific page and the server responds by sending it back. It travels across the network in lots of little packets back to the client where TCP put all the packets back in order. The web page is then reconstructed from the different sub-documents fetched (eg. text, layout description) and the browser renders the content. If the page has images or videos, the browser will see this and request that they are bought to the web page as well, one at a time. And ta daaa...just like that your web page has loaded!

Which brings us to the end of our whistle-stop tour from our starting point - the click of a link - to our destination - page load! Who knew there was so much going on behind the scenes? Next time you click on a link you'll know that it's not just magic...it's actually a series of complex protocols and interactions which happens between a number of computers all over the world. And the most amazing thing is that it happens in a matter of milliseconds! Which actually does sound like magic when you think about it. Super cool 🙂