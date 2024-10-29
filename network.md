# Network  

## The birth of the internet.  

### An Analog Version: Telephone Networks  

- Voice signals transmitted through analog electric signals.  
- **Circuit Switching**: Dedicated physical circuits established for each phone call. Remained until end of call.  
  - Guaranteed latency/throughput.  
  - Many points of failure, ie: a link or switch goes down.  
- **Electromechanical Switches**: Used relays for automatic call routing.  
  - physical devices that connected different wires to create a circuit.  
  - automatic call routing, reducing human intervention.  
- **Hierarchical Routing Structure**:   
  - Local exchanges connected phones within a local area.  
  - Tandem Exchanges: connected local exchanges.  
  - regional exchanges: connected tandem exchanges.  
  - long-distance Trunks: connected regional exchanges.  


### ARPANET: The First Internet @ Boelter 3420  

**Purpose**: Created by ARPA for resilient communication during the Cold War.  

- **Nodes**: Four initial nodes at UCLA, SRI, UCSB, and the University of Utah  
- ARPANET leased dedicated analog lines from telephone companies. Constant connection between points, unlike switched circuits used for regular phone calls.  
- **Modems**: ADC/DAC -> converts digital data from and into analog signals suitable for transmission over telephone lines. Converts back into digital data at the receiving end.  

1. **IMP (Interface Message Processors)**  
- **Function**: Acted as routers for the network.  
- **Responsibilities**:  
  - Receive messages from connected hosts.  
  - Store packets if necessary.  
  - Determine optimal routing paths.  
  - Forward packets to the next IMP on the path.  
- **Network**: Distributed mesh network, multiple paths between points. Resilient.  
2. **Host Computers**  
  - Each host is connected to the ARPANET through dedicated connections to their local IMP (Interface Message Processor).  
  - Heterogeneity: there is diverse range of host computers with different operating systems and hardware architectures. IMPs managed the complexities of interconnecting these diverse systems.  

3. **Packet Switching (by Paul Baran, RAND Corp, UCLA Alumni)**   
- **Message Breakdown**:  
  - Data is divided into small packets.  
  - Each packet includes:  
    - A header containing addressing information (source and destination).  
    - Sequence numbers to maintain order.  
    - Control data and byte sequences (header + payload).  
- **Independent Routing**:  
  - Packets are routed independently across the network.  
  - Each packet may take different paths depending on network conditions and available links.  
- **Reassembly at Destination**:  
  - The destination IMP reassembles the packets into the original message using their sequence numbers.  
- **Characteristics of Packets**:  
  - Best Effort Delivery: There is no guarantee that packets will arrive.  
  - Dropping: Packets can be dropped due to network congestion or errors.  
  - Out of Order Arrival: Packets may arrive in a different order than they were sent.  
  - Latency: There may be delays in packet delivery.  
  - Duplication: Packets can be duplicated, especially if a router is misconfigured.  
  - IMPs perform basic error detection on packets.  
 
#### ARPANET FLow:

1. A user on a host sends a message.  
2. The host breaks the message into packets.  
3. Packets are sent to the connected IMP, which:  
   - Receives packets (no guarantees on delivery).  
   - Examines the destination address.  
   - Consults the routing table.  
   - Forwards packets to the next IMP.  
4. The destination IMP reassembles packets and delivers the message to the destination host.  

## Modern Networking

### Internet Protocol Suite

Commonly known as the TCP/IP model. A combination of protocols, governing operation of the internet. Structured in layers that each serve a purpose.  

#### 1. **Link Layer (Network Access Layer)**  
- **Purpose**: Facilitates communication between adjacent nodes on the same local network.   
- **Function**: Handles physical transmission of data over network hardware.  
  - Physical Addressing: Uses MAC (Media Access Control) addresses to identify devices on the local network.  
  - Access Control: Determines how devices share the network medium (e.g., via CSMA/CD in Ethernet).  
  - Error Detection and Correction: Identifies and corrects errors in data transmission at the physical layer.  
- **Key Protocols**:  
  - Ethernet: The most common LAN technology, using a bus or star topology.  
  - Wi-Fi: Wireless networking standard, allowing devices to connect without physical cables.  
  - PPP (Point-to-Point Protocol): Used for direct connections between two nodes, often over serial links.  
- **Example**: A computer connecting to a router via Ethernet uses MAC addresses to identify itself on the local network.  

#### 2. **Internet Layer**  
- **Purpose**: Manages packet routing through the network, ensuring data is sent to the correct destination.  
- **Key Protocols**:  
  - **IPv4**: (Internet Protocol version 4) The most widely used version, providing an addressing scheme with 32-bit addresses (e.g., `192.168.1.1`).  
  - **IPv6**: (Internet Protocol version 6) Developed to address the limitations of IPv4, using 128-bit addresses (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).  
- **Packet Structure**:  
  - Version: Indicates the IP version.  
  - IHL: Internet Header Length, specifying the entire IP header's length.  
  - DSCP: Differentiated Services Code Point, indicating the type of service.  
  - ECN: Explicit Congestion Notification, info on the route (network) congestion.  
  - Total Length: Length of the entire packet (header + data).  
  - Flags: Control flags for fragmentation (e.g., "Don't Fragment").  
  - Fragment Offset: Indicates the position of the fragment in the original packet.  
  - Protocol: Tells the receiving internet layer what transport layer protocol this packet belongs to.  
  - Source Address: The IP address of the sender.  
  - Destination Address: The IP address of the intended recipient.  
  - Options: Optional fields for additional features.  
- **Example**: A web page request from a browser sends an IPv4 packet to the web server with the sender's and receiver's IP addresses.  

<img src="https://upload.wikimedia.org/wikipedia/commons/6/60/IPv4_Packet-en.svg" alt="IPv4 Diagram" style="display:block;margin-left:auto;margin-right:auto;width:60%;height:auto;">


#### **3. Transport Layer (Host to Host Layer)**  
- **Purpose**: Ensures complete data transfer between hosts, providing reliable or unreliable communication based on the protocol used.  
- **Functions**: Controls flow of data and reliable delivery.  
  - Segmentation and reassembly of data.  
  - Flow control.  
  - Error control (in TCP).  
  - Port addressing. Distinguish between applications on a host.  
- **Key Protocols**:  
  - **TCP (Transmission Control Protocol)**:  
	- Connection-Oriented: Establishes a connection before data transfer.  
	- Reliable: Guarantees data delivery through acknowledgments and retransmissions.  
	- Flow Control: Adjusts the rate of data transmission based on network congestion.  
	- **Example**: When downloading a file, TCP ensures all packets are received and assembled in the correct order, requesting retransmission of any lost packets.  
  - **UDP (User Datagram Protocol)**:  
	- Connectionless: Sends packets without establishing a connection.  
	- Unreliable: Does not guarantee delivery, order, or error correction.  
	- Thin layer over IP.  
	- **Example**: Streaming video uses UDP because timely delivery is more critical than perfect accuracy; lost packets are acceptable.  

#### 4. **Application Layer**
- **Purpose**: Interfaces directly with end-user applications, providing protocols for data exchange over the network. Assuming we can send reliable data, provides the interface for applications to access network services.  
- **Function**: Application-specific formatting and presentation. Session management. Interface with OS and applications.  
- **Key Protocols**:  
  - **HTTP (Hypertext Transfer Protocol)**: The foundation of data communication on the web.  
  - **FTP (File Transfer Protocol)**: Used for transferring files over the Internet, allowing users to upload and download files.  
  - **SMTP (Simple Mail Transfer Protocol)**: Protocol for sending emails.  
  - **DNS (Domain Name System)**: Translates domain names into IP addresses for identification.  
  - **DHCP (Dynamic Host Configuration Protocol)**: Assignes IP addresses and other paramters to devices on a network.  
- **Example**: A web browser uses HTTP to request web pages from a server, sending GET requests to retrieve resources and receiving HTML in response.
 
The Internet Protocol Suite is essential for ensuring that data is transmitted efficiently and accurately across the Internet, utilizing a layered approach to handle various aspects of networking. Each layer has specific protocols designed to address unique challenges in communication, enabling the seamless functioning of modern Internet services.  
 
### **HTTP (Hypertext Transfer Protocol)**  

An Application Layer Protocol!  

- **Requests**: Various types such as:  
  - GET: Requests data from a specified resource.  
  - POST: Sends data to server to create/update a resource (e.g., form submission).  
  - PUT: Updates an existing resource with new data.  
  - DELETE: Removes a specified resource.  
  - HEAD: Similar to GET but retrieves only headers.  
- **Responses**: Include status codes that indicate the outcome of the request  
	- Status: `200 OK`, `404 Not Found`, `301 Moved Permanently`, `500 Internal Server Error`.  
	- Headers: Information about response, content type, length, caching directives.  
	- Body (Optional): Contains requested data if any. (HTML, images, JSON)  
- **Versions**:  
  - **HTTP/1.0**: Single requests with no persistent connection. Inefficient because new TCP connection per request involves a lot of overhead.  
  - **HTTP/1.1**: Supports persistent connections and chunked transfer encoding, allowing multiple requests over a single connection.
	- Virtual Hosts: a single web server can host multiple domains on the same IP address. Differentiates requests based on domain name provided. Cost effective for server management.  
	- Pipelining: Clients can send multiple HTTP requests without waiting for corresponding response.  
		- Limitations in 1.1: Potential head-of-line blocking, where first request must be completed before processing subsequent requests.  
  - **HTTP/2**: Introduces multiplexing and header compression, improving performance.  
	- Multiplexing: multiple streams of data over a single connection simultaenously. Each stream is independent. Don't need to return in order.  
	- Elimanted head-of-line blocking issues for pipelining by allowing multiple requests/responses to be interleaved.  
  - **HTTP/3**: Built on QUIC, enhancing speed and reducing latency, especially for streaming.  
	- Good for streaming, better latency.  
	- More multiplexing built on UDP not TCP.  

### Browser Rendering

#### HTML  
The content retrieved via HTTP.  
- **Origins**: SGML (Standard Generalized Markup Language, IBM)  
  - Too complex: too flexible for the web and complexity slowed down browsers.  
- **Declarative**: HTML is a declarative language.  
  - Describes structure and presentation of text. (HTML, SGML, XML)  
	- 對方: Imperative. Gives instructions for a computer to perform.  
- **Elements**: Corresponds to a node in the tree that represents the document.  
  - Tags `<tag> ... </tag>`. Each element is written as a tag.  
	- A void element `<tag/>` cannot have any child nodes.  
	- A tag has attributes, treated as data stores in the treenode.  
	  - ie: `tag attr="val" attr2="val2"/>`.  
- **DTD**: (Document Type Definition)  
  - Used to define the structure and elements of HTML documents.  
  - Standardized way to validate HTML.  
  - maintained by W3C, and used in HTML 1-4.
	- When new elements were needed, DTD needed to undergo a formal organizational process.  
  - HTML 5: Moved away from strict DTDs, a more flexible and evolving standard.  
	- Faster innovation, more forgiving of errors, wider range of document structures.  

#### XML (eXtensible Markup Language)  
  - XML is a standard syntax for data representation. A branch of SGML developed by W3C and SGML.
- **Features**:  
  - Syntax: XML uses a syntax similar to HTML but does not include built-in elements. We define our own elements to suit our specific data structure.  
  - Primarily concerned with data storage and transport.  
  - Structure: Uses angle brackets for markup.  
  - Data Representation: Send hierarchical data (trees) over communication links.  
  - Primarily used for data storage and transport, not presentation.  

#### DOM Document Object Model  
  - The DOM is a spec that describes the tree data structure used to represent HTML and XML documents.  
- **Functionality**:  
  - Element Access: Provides methods for accessing element attributes and child elements.  
  - Navigation: Allows for navigation through the hierarchical tree structure of the document.  
  - APIs: Offers APIs for building, searching, and editing trees. JavaScript is the most popular language for interacting with the DOM.  
  
<img src="https://www.w3schools.com/js/pic_htmltree.gif" alt="IPv4 Diagram" style="display:block;margin-left:auto;margin-right:auto;width:60%;height:auto;">

#### CSS (Cascading Style Sheets)
- CSS is used to separate data from presentation, managing the style and visual aspects of web documents.  
- **Benefits**:
  - Consistency: Enables the application of styles consistently across multiple pages through external stylesheets.  
  - Flexibility: Provides control over every aspect of visual presentation, for richer UX.  
  - Responsiveness: Facilitates design of websites that adapt to different screen sizes and devices.  


#### Javascript
- JavaScript serves as a dynamic programming language. Allows for imperative coding within HTML documents.  
- **Features**:
  - Dynmic scripting: execute code directly in browser.  
  - DOM Manipulation: Can dynamically alter DOM trees, enabling interactive web applications.  
  - Asynchronous Programming: techniques such as AJAX allow fetching of data from servers without reloading entire page.  
- **JSON**: (JavaScript Object Notation) a lightweight alternative to XML, offering a smaller and easier-to-use data format. Used for data interchange. Easy to write and read.  
- **Limitations**: "Fails the CSS DOM hope"  
  - An ideal of using JavaScript to create complex layouts and styles that could be more efficiently handled by CSS. JavaScript's imperative nature can sometimes lead to less efficient and less maintainable code.  
  - Javascript execution can block rendering, performance bottlenecks.  

#### JSX (Javascript XML)  
- A syntax extension for JavaScript that allows you to write HTML-like code within JavaScript files.    
- Primarily used in React apps.  
- **Pros**:  
  - Readable: Easier to understand than nested JS functions calls when creating UI elements.  
  - Maintainable: Simplifies creation/management of UI structures.  
  - Type checking: catch errors earlier.  
- **Cons**:  
  - Learning curve for people new to JSX, how to integrate with JS.  
  - Build process: requires a build step to transform into normal JS.  
  - Debugging: Error messages could refer to compiled JS not original JSX.  
  - Verbose: For simple UI elements, more verbose than plain JS (or template literals)  
  - Tightly coupled with React.  
  
#### Browser Rendering Pipeline
- **Process Overview**: The rendering pipeline transforms HTML, CSS, and JavaScript into a visual display as follows:  

> **HTML + CSS + JavaScript** →  
> **DOM + CSSOM** (Parsing)→  
> **Render Tree** (Rendering)→  
> **Layout** →  
> **Paint** →  
> **Composite** →  
> **Visual Display**  

1. **Parsing**:  
   - HTML Parsing: Converts HTML into the **DOM** (Document Object Model).  
   - CSS Parsing: Converts CSS into the **CSSOM** (CSS Object Model) tree structure.  
   - JavaScript Compilation: JavaScript can modify the DOM and CSSOM, potentially requiring re-rendering to reflect changes.  
2. **Rendering**: Browser combines DOM and CSSOM to create the **Render Tree**. Represents the visual structure of page: contains only the visible elements.  
3. **Layout**: Browser calculates the size and position of each element in the Render Tree, determining the geometric layout of the content.  
4. **Paint**: Browser draws pixels for each element on the screen, including:  
   - Filling colors  
   - Applying background images  
   - Drawing borders  
   - Rendering text  
6. **Composite**: Elements in the page may be layered; the browser composites these layers to create the final visual representation.  
   - Compositing can enhance performance, especially during animations and transitions, as changes to a single layer do not necessitate repainting the entire page.  
7. **Incremental Rendering**:  
   - The browser can begin rendering an element as soon as it encounters the opening tag, allowing for a quicker but incomplete display of the webpage.  
   - ie: ` <story headline="Big Long Demo"> 3GiBs </story>`  
     - The browser guesses the layout and decides to ignore off-screen elements initially.  
     - Attributes with low priority are executed last.  
     - Rendering of tables may trigger a "refresh" of the screen, leading to JavaScript execution multiple times.  
  
### Code Examples

#### HTML and CSS:  

	<!DOCTYPE html>
	<html>
	  <head>
		<title>My Styled Page</title>
		<link rel="stylesheet" href="style.css">
	  </head>
	  <body>
		<h1>This is a heading</h1>
		<p>This is a paragraph.</p>
	  </body>
	</html>
	
	/* style.css */
	h1 {
	  color: navy;
	  font-size: 32px;
	}
	p {
	  color: gray;
	  line-height: 1.5;
	}


## Application Styles

#### Standalone Applications

A standalone app (also known as desktop app or thick client) runs on a single computer, doesn't need a network connection for its functionality. Processing, data storage, and resources on host device. (ie: Word, Photoshop, a calculator app).  

- Pros:  
  - performance is fast, responsive, don't rely on network speeds.  
  - work without internet connection.  
  - data is private to machine.  
- Cons:  
  - Little collaboration - sharing data is manual.  
  - Potential version inconsistencies since each user installs updates independently.  
  - Resource intensive: CPU, memory, storage.  
  
#### Client Server Applications

Two programs, a client and a server. Client presents information to the user, requesting data and services from the server. The server handles data processing and storage. (ie: email, social media, banking).  

- Pros:  
  - Data is centralized. Accessible from any client.  
  - Multiple clients can access and modify data, collaborative.  
  - Updates are easy: server admin just needs to update software.  
- Cons:  
  - Depends on network, needs stable internet.  
  - If server is overloaded, performance might suffer.  
  - Centralized data means a single point of failure for security breaches.  
  
#### Peer-to-Peer Applications

Each computer acts as client and server. Resources are shared mutually without a central server. Connect to multiple servers. (ie: BitTorrent).  

- Pros:  
  - Decentralized, no single point of failure. Operational even if peers disconnect.  
  - Scalable. More people means more capacity.  
  - Efficient distribution. Ie: large files downloadable faster by pulling from multiple sources.   
- Cons:  
  - Security risk: vulnerable to malware.  
  - Performance may fluctuate depending on number of peers and connection speeds.  
  - Difficult to manage and monitor the network, without central control.  
  


