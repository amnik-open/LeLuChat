# Architecture
LeLuChat consists several microservices that work together. Simple architecture can be seen in below
diagram:

![LeLuChat Architecture](LeLuChat.png)

Next section will explain each microservice:
## [Auth](https://github.com/amnik-open/LeLuChat_Auth)
This microservice is responsible for authenticating different types of users. Arsenal microservice 
implement authentication middleware that transfer http request to Auth, for authenticating 
different requests that come from users.  
Auth accept two different RPC call from Arsenal:
### WebsiteUser registeration
Every user come to website that wants to create chat should be registered first. So Arsenal send 
this RPC request to Auth to create WebsiteUser object.
### LeLuUser Membership
LeLuUsers should be enabled to become member of Room. So Arsenal get information about these 
users with this RPC call from Auth.
## [Arsenal](https://github.com/amnik-open/LeLuChat_Arsenal)
This microservice store all messages, chats and rooms data. It also provides APIs for different 
operations of admin panel. It accepts rpc call from Messaging service to store messages permanently 
from websocket. It also acts as a messaging gate for Messaging service, to authenticate and 
authorize users that send request with websocket of Messaging.
## [Messaging](https://github.com/amnik-open/LeLuChat_Messaging)
Messaging is implemented with django channels that provide websocket. With this microservice, 
WebsiteUsers can chat with LeLuUsers in the website.
