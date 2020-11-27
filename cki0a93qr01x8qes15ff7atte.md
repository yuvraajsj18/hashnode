## Do You Understand the Internet?

We use the internet on a daily basis. Our phones, laptops, computers, all connected to the internet. But how the internet works? 

In this blog, we are going to find the answers to these questions -

- What is the internet?
- What is a network?
- What are IP addresses?
- What happens when you search on Google?
- What are the rules of the Internet?
- Where is Google’s server located?
- What devices hold the internet together?

> Fasten your seat belts for a ride over routers...


## What is the Internet?

- The Internet is the global system of interconnected computer networks that uses the Internet protocol suite (TCP/IP) to communicate between networks and devices.
- It is a network of networks.
  - Several collections of computers together make the internet.
- It is used for sharing various resources such as web pages, emails, file sharing.
- To understand the internet, we first need to understand what a network is?


## What is a Network?

- A network is a collection of computers, servers, mainframes, network devices, peripherals, or other devices connected to one another to allow the sharing of data.

- Consider an example of a network: your **home network** -

  - You have a router in your home.
    - This router connects to the Internet.
    - You pay your isp for this connection - Airtel, Jio, etc.
    - Other devices connect to the router with cables or wifi.

![Home Network](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481227664/iRg8XvpCK.png)


## What are IP addresses?

- Every device on the internet has an IP address that allows other computers to talk to it.
- It is of the form: #.#.#.#
  - Four numbers separated by dots of the values 0-255.
  - This version of IP addresses is called **IPv4**.
- Like postal addresses, they uniquely identify computers on the internet.
- ISPs assign an IP address to your router.
  - Earlier, it is used to be physically configured.
  - Today, it is assigned automatically using a [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) Server that lives in ISP.
- But, if your ISP only assigns one address to the router, how are you able to connect multiple devices to the internet?
  - That’s because your router assigns **private IP addresses** to the devices.
  - This private IP address is free and reserved for this use only.
  - These are the private IP address ranges:
    - 10.0.0.0 – 10.255.255.255
    - 172.16.0.0 – 172.31.255.255
    - 192.168.0.0 – 192.168.255.255


## What Happens When You Search on Google?

With an IP address assigned to us, we are officially on the internet. Now we can communicate with other devices on the internet. So, let's try to talk with Google Servers.

We will open software called a browser (like chrome) and enter a query to search with Google’s search engine. The browser will do the job of converting our normal query to a proper HTTP request to google.

- Suppose we searched for cats, our request will look like:

  `GET /search?q=cats HTTP/1.1`

Computers communicate by sending **packets,** which are like **virtual envelopes** sent between computers. (Ultimately still 0s and 1s).

So we will place this request inside an envelope (as an analogy). On the envelope, we need to mention the destination and source address.

- We know our IP address.
- But we don’t know the IP address of Google…?

But we do know the domain name of Google - [www.google.com](http://www.google.com). To convert a domain name to its corresponding IP address, we use a **Domain Name System(DNS) server.**

A request will be sent to the ISP’s DNS server for Google’s IP address.

- If the ISP’s DNS server doesn’t know a website’s IP address, it has been configured to ask another DNS server.
- There exist root servers that know where to look to for an IP address if it exists.

![Packet as envelope](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481287984/07SvHMUln.png)

We have assumed our IP to be 1.2.3.4 and google’s 5.6.7.8. After sending the request off, we’ll get a response some milliseconds later. The result will be sent back in **one or more** packets.

- If the result is too large for a single envelope, sending it in one packet could take up the internet traffic.
- To solve this, Google will divide the result into smaller fragments (say 4).
  - Put the fragments into different envelopes.
  - Write information on the envelopes:
    - Return address: Google IP address
    - Delivery address: Our IP address.
    - List the number of packets on each envelope (1 of 4, 2 of 4, …).

**What if one of the packets goes missing?**

We can logically infer which packet is missing based on the ones received. For this, we will need another protocol called **TCP (Transmission control protocol)** which ensures packets can get to their destination.

It supports **sequence numbers** that help data get to its destination.

- When missing a packet, a computer can make a request for the missing packet.
- The computer will put packets together to get a whole file.

This protocol also includes conventions for requesting services (**port identifiers).**

- To make sure Google knows we’re requesting a web page and not an email or other service.

If 5.6.7.8 is Google’s IP address, 5.6.7.8:80 (port 80) specifies that we want a webpage.

- 80 means **HTTP (Hypertext transfer protocol).**
  - **The language web servers speak.**
- Emails use port 25 - SMTP.
- Secure connection use 443 - HTTPS.

**Therefore, on the envelope we previously saw, we must have mentioned the port as well before sending it.**



## What are the Rules of the Internet?

We have used the term **protocols** multiple times till now. Protocols are just sets of rules.

- Humans use these all the time, such as the protocol for meeting people: handshakes. (pre-corona times!!)

Internet uses these protocols to standardize all communication. 

- HTTP, FTP, TCP/IP, etc.

There is one more protocol called **UDP** (User datagram protocol) that can be used instead of TCP.

- It doesn’t guarantee delivery.
- Used for video conferencing.
  - Packets can be dropped for the sake of keeping the conversation flowing.

- Used anytime you want to keep data coming without waiting for a buffer to fill.



## Where is Google's Server Located?

When we sent our envelope, our laptop didn’t know where is the Google’s server located. We knew the IP address of the server but we didn’t have a map to decide which direction to go to and we certainly cannot use Google maps 😅.

This again is the job of routers:

- Routers have a big table with IP addresses and where data should be routed to get to that destination. Often, the data is routed to the next router.

The router’s purpose is to send data in the direction of a destination. The next router will send it to another until it reaches a destination.

The routing decisions are made using certain routing algorithms such as **Dijkstra’s shortest path algorithm or distance vector routing algorithm.**

![laptop-routers-google](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481398222/m8Slahxgn.png)

We can use a program called **traceroute** that sends packets to each router on a path to a destination, reporting the time it takes to reach that router:


![traceroute to www.google.com](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481426890/uUPFyuo0U.png)

- It took us 13 jumps to get to google finding our way through routers.
- Also, Now we can see Google’s IP address is not 5.6.7.8 but 142.250.67.68.
- It took us only 42.130 ms to get to Google!!!



## What Devices Hold the Internet Together?

- **Undersea Cables:** A submarine communications cable is a cable laid on the sea bed between land-based stations to carry telecommunication signals across stretches of ocean and sea.

  Check out this video to see the network of undersea cables around the world:

  %[https://youtu.be/IlAJJI-qG2k]

- **Cable Modems:** A cable modem is a hardware device that allows your computer to communicate with an Internet service provider over a landline connection. It converts an analog signal to a digital signal for the purpose of granting access to broadband Internet.

  - Coaxial cable to plug into the wall.
  - Phone jacks (RJ11) as many services are bundled together these days.
  - Four jacks for ethernet cables (RJ45).
  - Devices can plug into these for internet connectivity.

![a RJ45 cable](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481619700/nwr0lGumO.png)

![a cable modem](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481594636/sVi8_7LpU.png)

- **Switch**: A network switch is networking hardware that connects devices on a computer network by using packet switching to receive and forward data to the destination device.


![Switch](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481542710/wL3a33ptf.png)

- **Router**: A router is a networking device that forwards data packets between computer networks. Routers perform the traffic directing functions on the Internet. Home routers can have wifi, firewall, and switching capabilities.


![Router](https://cdn.hashnode.com/res/hashnode/image/upload/v1606481566218/9RkvWpo32.png)

### Thanks For Reading 😊

If you found this article helpful, please like and share!
Feedbacks are welcome in the comments.

---

#### You may also like:

- [What Happens When You Run a Computer Program?](https://blog.yuvv.xyz/what-happens-when-you-run-a-computer-program)
- [The Mutable Default Argument Mess in Python](https://blog.yuvv.xyz/the-mutable-default-argument-mess-in-python)
- [Modern C++ Features](https://blog.yuvv.xyz/modern-cpp-features)
- [Comprehensions in Python: Explained](https://blog.yuvv.xyz/comprehensions-in-python-explained)

Connect with me on [Twitter](https://twitter.com/yuvraajsj18), [GitHub](https://github.com/yuvraajsj18), and [LinkedIn](https://www.linkedin.com/in/yuvraajsj18/).

This article is inspired by a presentation I gave with my friend [Manmeet Brar](https://www.instagram.com/manmeet_brar_._/) in my Computer Network class.
You can find the presentation here: [slideshare](https://www.slideshare.net/YuvraajSinghJadon/internet-239539082)
