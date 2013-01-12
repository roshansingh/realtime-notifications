realtime-notifications
======================
If you are making a web application which needs to update client in realtime, you can use this example to quickly write such an application in `nodejs` using `socket.io`. `Redis pubsub` is used as a data source in this example. You can use any other data source. 

Since these kind of applications are event-driven on server side (for example, a new message arrived for user) it is a good idea to use nodejs.

Socket.io(http://socket.io) is used to maintain connection with the user. It uses websockets if available else uses fallback machanisms like long-polling. For more details see https://github.com/LearnBoost/socket.io-spec

## Requirements
* redis
* nodejs
* nodejs redis module 
* nodejs socket.io module

## Installation
For installing `redis` visit http://redis.io/download

For installing `nodejs` visit http://nodejs.org/download

If you are on linux, you can use package manager of your distribution to install `redis` and `nodejs`.

Use npm to install nodejs dependencies

	npm install redis socket.io

You may want to use `hiredis` on production as explained on project page https://github.com/mranney/node_redis.

## Usage
Start the server by 

	cd server
	sudo nodejs server.js

Now hit `http://localhost` on your browser

## Server side flow
When the server starts, an http handler is created whose only task currently is to server index.html. 

There is socket.io handler which listens to all the websocket connections and manages them. It subscribes them to appropricate rooms and sends updates.

Lastly there are two redis clients one of which subscribes to channels on redis and as soon as a message is received, it broadcasts them in appropricate rooms. The second client simply publishes dummy updates to redis channels to which the first redis client is subscribed to.

## Client side flow
As soon as the page load is done, socket.io client tries to connect to the server and on connection sends subscribe message for a particular channel. When updates are received it displays them

I have documented the code as extensively as I could. Please email me in case of doubts.  