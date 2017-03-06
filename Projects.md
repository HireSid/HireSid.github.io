### Service Discovery Registry for etcd - Node.js (~March 2015) (GitHub) (npm)
This is a service discovery daemon written in Javascript/Node.js for CoreOS/Fleet. Part of the problem in building a distributed systems architecture is discovering and addressing specific micro-service endpoints that form that architecture. There are very many container orchestration engines now - Docker Swarn, CoreOS, Kubernetes, Apache Mesos. All of these have some form of service discovery mechanisms that will allow services to announce their own endpoints and clients to retrieve and connect into these endpoints.

This package is a node.js library hosted on npm. The library allows the developer of a micro-service to very succinctly register a service against etcd(a distributed RAFT-based consensus key-value datastore) to be made available across the fleet in a distributed system. The library also allows the client/consumer of a micro-service to discover the endpoint IP and port with a simply string name for that service. 

I later also built a side-kick service on top of the library that can be run as a CLI tool that monitors the service being registered. The monitor will heartbeat the TCP port of the service and automatically de-register the service from etcd whenever that service is no longer accepting connections. Removing 'bad' instances out of the fleet quickly is a crucial part of a self-healing distributed system. 

Think of this as a foreverjs or supervisord, but in a distributed systems architecture that uses containers to componentize the individual pieces.

I built this service during the early days of buddybuild - when we were still trying to understand how to architect the cloud build system. We ended up not using the registry library - since we decided to not use CoreOS/etcd. However, the library lived on and sees a decent amount(~100) of downloads every month.


### DashHooks - Node.js (Sep 2015) (GitHub) (npm)
This is a simple server written in Javascript/Node.js that intercepts button presses on the Amazon Dash Buttons and triggers a command-line script. This was when the Amazon Dash button was first launched, and the idea of just triggering actions on the internet with a single physical button press fascinated me.
 
Amazon did not offer any sort of API for the Dash Button. The Dash button comes pre-configured to connect into a WiFi AP and then fire off a HTTP call to a hardcoded URL that is hosted on the Amazon.com domain. Typically, the URL endpoint is routed to trigger a 'buy' action for the account owner. But If you do not set a product to be ordered on the account, that buy action HTTP call is a no-op.

So I took advantage of the fact that the button first needs to connect into WiFi every time it's pressed, regardless of whether it is configured to buy anything. As it connects into the WiFi network, it sends out an ARP message to all clients on the same AP to discover the gateway address. The server I built intercepts that ARP message and then fires off a configurable command-line script.

With the server running somewhere under the same network, you could now set up any sort of command line script. The intended use case was to fire off a cURL request as a webhook to trigger an action on a different service. Although I didn't have a specific use-case in mind, the library sees a decent number(~50) of downloads a month - so I suspect someone is benefiting from this effort.

We later used this button to order sandwiches from a local sandwich shop in Vancouver - which brings us to my next project.

### Sammie - Node.js + Express.js + Casper.js (Aug 2015) (GitHub)
This was a hackathon project that Johnny(a buddybuild co-worker) and I built over a weekend. This was a sandwich ordering app. The app was simple. One button. When pressed, it orders a Sandwich from Hubbub (a healthy salad and sandwich shop that buddybuild employees unanimously love). Johnny worked on the iOS app. I worked on the express.js and node.js backend.

The backend did all the heavy lifting in terms of ordering the sandwich from the shop. Hubbub has an online ordering page. It's so clunky that simply walking into the shop is way faster than navigating the UI they have. I scripted the website UI (specifically the buy pipeline) with Casper.js. The hackathon implementation was hard-coded to use my credit card and used a pseudonym "Russel Rains" - which is the fake persona we use in buddybuild as our test user.

The iOS app sent a POST request to the backend. The backend then navigated the Hubbub website through Phantom.js/Casper.js and ordered the sandwich. We would then walk to the shop and pick up the sandwich. The experience was magical. No waiting in line. No credit card. No signature. Press button. Walk to shop. Pick up sandwich. Eat.

This was a massive time saver - since we are a startup, every minute saved was incredibly valuable for us. A month later, we hooked up DashHooks into the Sammie backend.

But since the app only orders one very specific type of sandwich, we grew bored of it, eventually and we stopped using it.


### OS Process Scheduler in C (GitHub)
This is an OS process scheduler I wrote as part of a school project in C. This project was a line-item in a series of assignments that were meant to be load-balanced across a team of four people. I took on the majority of this one work item while the rest of the line-items were split across the other team members.

This project is intended to simulate a multi-level feedback queue time-quantum process scheduler that is part of any modern pre-emptive multi-tasking operating system.

This code is well designed and documented. I am showcasing this code even though it is 5+ years old, because I specifically remember Abhi and Doug mentioning that there was some part of the stack written in C/C++.


### Gravity Simulator - C++ + OpenGL + MFC (GitHub) (Video)
This project was a part of a physics course in university. The project goal here was to simulate Newtonian gravity interactions between N bodies and have the results charted into 2D graphs of the movement of planetary bodies. I decided to change up the project requirements a little bit and use the opportunity to learn about graphics programming - specifically OpenGL. 

The project simulates n-body interactions between planetary and stellar bodies. It then uses the results of the simulation to render a scene graph in OpenGL + MFC. A lot of work also went into performance tuning as n-body simulation is inherently an n^2 algorithm.