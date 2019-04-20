+++
date = 2019-04-17
linktitle = "noebs: the most secure middleware"
excerpt = "We introduce noebs, a free open source payment gateway"

tags =  [
	"noebs",
	 "electronic-payment",
]
prev = "/tutorials/mathjax"
title = "noebs: the most secure middleware"
weight = 10
+++

>API-first, high performant middleware. noebs is the most secure and modern middleware.
# What is noebs

It is definitely not a replacement for EBS, if anything we embrace the use of EBS and its role as a unified switching system. But, we aim to provide a thin wrapper around EBS functionalities that can be exposed to both POS and mobile applications. A starting point where you can write your business logic. It is free and open source built using Go. noebs encapsulates many of the things I learned while working with a full fledged payment gateway. It is very fast and robust and doesn’t get on your way while using it. The design of noebs makes it very simple for the developers to work with and extend it. It is not opinionated, we assume that the developers know better what their business needs and tailor noebs to their requirements. You can add as much of other middlewares as you wish; be it a logger, sms gateway or any other service. We highly encourage you to adapt this microservice architecture, where the whole application is layered on top of each other’s.

## This project goals

Provide a highly scalable payment gateway that can handles tens of thousands of concurrent requests. Currently, we are only interfacing with EBS, but we plan to cover other private switches as well. It is also open source meaning you can use for free! We don’t have any hidden subscription fees or anything. Totally free and open source.

## Commercial plans

We do have commercial plans. In fact, we can help you in every part of your electronic payment system. You can use our hosted middleware service without the need of hosting it yourself.

- EBS simulator (you can use it in during your development phase)
- We also have QA developers that can help you during your tests. They’re as lame and bureaucratic as EBS ones are
- we can help you write your clients applications, whether they’re mobile, or POS
- we can assist and help you plan for your business model

For more details, contact us at mmbusif@gmail.com.

## Why Go?

Go is really fast! Our application can happily serve more than 60k req/sec. The bottleneck will never be on your payment gateway service! Plus, Go helps with many of the problems I faced while working with Python, the static typing can prevent your errors from occurring only at runtime, and your code will compile into a single binary that you just run. I’ve been very excited to write web services Go and this project offers me just that!

# How to use noebs
There are different ways to use noebs:

## Building using Docker and docker-compose
We provide an easier way to build and run noebs using Docker.
- Fork this repository (e.g., `git clone https://github.com/adonese/noebs`)
- `cd` to noebs root directory (E.g., $HOME/src/noebs)
- `docker build -t noebs .`  # -t for giving it a name
- `docker run -it -p 8000:8000 noebs:latest`
- Open `localhost:8000/test` in your broswer to interact with noebs


## Building with go get command [not recommended]
- make sure you have Go installed [Consult go website to see various ways to install go](https://golang.org)
- Then
```shell
# this command may likely takes along time depending on your internet connections.
# also, make sure you are using a vpn since some of the libraries are hosted in GCE hosting which forbids Sudan
go get github.com/adonese/noebs
cd $GOPATH/github.com/adonese/noebs
go build .
```
You will have a binary that after running it will spawn a production ready server!

## Notes on installation
noebs needs to be connected with EBS merchant server in order to get useful responses. *However, you can run our embedded server that mocks EBS responses in cases where you cannot reach EBS server*. To do that, you need to enable the development mode using a special env var, `EBS_LOCAL_DEV`. You need to set `EBS_LOCAL_DEV=1` in order to use the mocking functionality.

- Using Docker
```shell
docker run -it -p 8000:8000 -e EBS_LOCAL_DEV=1 noebs:latest
```

- Using `go get` method
```shell
export EBS_LOCAL_DEV=1 noebs
```

# This project philosophy
noebs is not meant to be a full e-payment framework (e.g., unlike Morsal). It is meant as a generic e-payment gateway system. Currently, it implements EBS services, but we might add new gateway. Being such, adapts to Unix philosophy; doing one thing and do it good. Also, with our experience with embedded devices, working with authorizations and handling all of these headers and tokens (esp. JWT ones) has proven to be challenging as simply some of the older models cannot handle lengthy headers.
You can however have this system architecture, suppose that you're building a mobile payment application system:
- a mobile application app (with its backend system, obviously). This app will encapsulates the business logic and authenticate the incoming requests.
- a chatting service. Like WeChat, where people can send their money to their friends and families, in a very friendly way.
- ecommerce platform. The idea is _not_ just to offer an epayment gateway, well, EBS offers that through their MCS web services.
- and finally the payment gateway layer which handles the payment part.
- there could be other services e.g., push notifications, SMS, 2FA and plenty of others.
- logging and the reporting system.
- rate limiting, geographical blocking and other API gateway protections.
All of these will be implemented in a microservice archiectural design pattern, and it is your decision to choose what services you want. A mobile payment provider can use our payment service inside their application whenever their users are requesting any transactions. _It is not our responsibility to authenticate your users_. This way, we can use this application in virtually any place. Our client consumers are held responsible for providing any kind of authentication for their requests.


## Services we offer
noebs implements *ALL* of EBS merchant services. We are working to extend our support into other EBS services, e.g., consumer services, TITP, etc. However, those other services are not stable and some of them (consumer) are deem to deprecation.

If YOU are interested in other services, please reach out and we will be more than happy to discuss them with you.


# Consultancy
While everything you see here is very and open source; we don't hide any fees or charges, we expect that some might be interested in a commercial plans. We offer our consultancy services via Gndi. We have a team with variety of proficiency, from backend engineers, mobile developers to UX/UI and QA testing engineers. Some of our team members have worked at EBS, while most of the team have a huge experience in e-payment systems.

Contact us: +249 925343834 (Mohamed Yousif) | +249 9023 00672 (Mohamed Gafar) | adonese@acts-sd.com (Mohamed Yousif)

# Our simulator and EBS services
Our team have developed an internal EBS QA test system that emulates EBS test environment. We offer our simulator as a paid service 
- very superior to that of EBS testing server. It runs on weekends. Well, 24/7, just like any server should work ¯\\_(ツ)\_/¯.
- hate EBS's bureaucracy? We do too. No need for the EBS busy servers, you can test our server at any time.
- we have two plans for the simulator: 
	- you can use our EBS simulator on your own; we won't test your services.
	- we can use our EBS simulator while we do the plan for you, the exact way EBS does. Bear in mind that our testers are highly competitive and they're all ex-EBSers.

**We plan on releasing our simulator very soon. Stay tuned.**
