---
author: linaro
comments: true
date: 2016-09-06 20:01:17+00:00
layout: post
link: https://www.96boards.org/blog/recap-of-the-96boards-openhours-17/
slug: recap-of-the-96boards-openhours-17
image: /assets/images/blog/OpenHours-03.png
image_name: OpenHours-03.png
title: Recap of the 96Boards OpenHours 17
wordpress_id: 17143
Boards:
  - DragonBoard 410c
  - HiKey
category: blog
tags:
  - 64-bit
  - 96Boards
  - aarch64
  - Android
  - ARM
  - ARMv8
  - Breakout
  - bubblegum-96
  - CE
  - Consumer Edition
  - Consumer IoT
  - DB410c
  - debugging
  - dragonboard410c
  - gdb
  - gui
  - HiKey
  - Library
  - Linux
  - Low speed expansion header
  - Open Embedded
  - Open Hours
  - OpenHours
  - Reference Platform
  - rpb
  - sensors
  - UART
---

96Boards OpenHours just had it's 17th episode and it is continuing to grow.  This week was our largest audience to date.  OpenHours is a chance for those in the 96Boards community to come every Thursday to learn and ask questions about 96Boards.  We are currently between seasons so this hour is available for those that call in to ask questions of the many developers we have on the call.   This week's episode began with Robert making the announcement that we will be giving away some Dragonboards in September during one of our OpenHours sessions.   It will be during a 3 part series that will begin on Thursday September 15th, the first episode will be about simple unboxing of a new DragonBoard 410c, the second episode will be a demo with Lawrence King from his desk at Qualcomm Canada (during this episode we will be taking down names for those that want to be part of the drawing) and the final part of the series will be a live panel at our Linaro Connect event in Las Vegas, Nevada to discuss the DragonBoard and to answer any questions (and we will announce the winners).  After the give-away announcement Robert opened the call up to any questions the participants had.  To watch this weeks’ session go to [(https://www.youtube.com/watch?v=FNF-AL-wkN0)](https://www.youtube.com/watch?v=FNF-AL-wkN0)

{% include media.html media_url="https://www.youtube.com/embed/FNF-AL-wkN0?feature=oembed" %}

- The first question was regarding the DragonBoard give-away and participation.  More details to come.

- Then there was a question about what does the Amazon SDK allow us to do in particular? Also is there a way to connect to Watson?  Robert suggested a couple of links to refer to that you can see in the chat below.  The team was also contacting a team member to join to try to address the questions in more detail.  Robert also gave out his email to contact him directly with questions.

- The next question was for the coursera students, is there a list of sensors and/or other accessories they will need?  The short answer is yes, there is a list of accessories but check out the list of materials that is listed at the end of course 2 and the beginning of course 3.

- There are now kits on seed studio that you can find the correct sensors.   Next was a follow-up question about what are the list of accessories one needs to buy along with the board?  The cost of the sensor kit is $69 (from Seed studio) and can be delivered to many locations. [http://www.seeedstudio.com/depot/Grove-Starter-Kit-p-709.html](http://www.seeedstudio.com/depot/Grove-Starter-Kit-p-709.html).  Also something to keep in mind is that with AWS kit the board is already loaded with Debian and a power supply.   [https://github.com/ArrowElectronics/aws-iot-device-sdk](https://github.com/ArrowElectronics/aws-iot-device-sdk)

- There was a guest participant that was interested in the possibility of Yocto Project with dragon board. What is the status of the support as of now?  You can find information about the DragonBoard on [https://www.96boards.org/product/dragonboard410c/ ](/product/dragonboard410c/) and [https://github.com/Linaro/documentation](https://github.com/Linaro/documentation)

- Robert then answer a question about what 96Boards and DragonBoards are being developed for.  He talked about different applications that the boards were being used for.  Lawrence then discussed how DragonBoard gives engineers a path to production and how it makes the board easier to get your ideas to market.

- There was a question on what are the concerns/considerations for running the Dragonbaord from a battery?  Alkaline/Ni-Cd/Lithium?  The team discussed what was available and what runs the best on the DragonBoard.

- The next question was about what operating environments these work in. How hot and how cold an environment can these operate in? Also, EMF fields/interferance?  Lawrence discussed then the different conditions regarding the operating environments that it can tolerate.

- Can you use the DragonBoard as a data acquisition and control device?  The short answer is yes but there are limitations that Lawrence and David discussed.

- Robert closed the call talking about the blogs that are available and can be found here:  [https://www.96boards.org/blog/](/blog/)

As always there is a lot of good information and resources that is in the chat below, this is a great place to get more detailed information.  Also a while ago in the hangout Robert shared a link to allow people to submit topics or questions for the developers on the hangout.  The link is:[ https://discuss.96boards.org/t/openhours-topic-suggestion/ ](https://discuss.96boards.org/t/openhours-topic-suggestion/)and Robert will take these suggestions and try to incorporate these into future OpenHours.

Don't forget about the upcoming Linaro Connect where attendees have an opportunity to meet with Linaro in person and learn a lot more about what is going on in the community.  There are still openings available to attend this conference in Las Vegas, Nevada September 26-30, 2016 --[http://connect.linaro.org/](http://connect.linaro.org/).

Be sure to join us for the next OpenHours  [https://www.96boards.org/](/)  where we will go through an out of box experience with the DragonBoard 410c.

Please remember, if you get stuck, there are resources to help you through the installation. Feel free to check out the [96Boards forums](https://discuss.96boards.org/), [96Boards wiki](https://github.com/96boards/documentation/wiki), or [Freenode IRC](http://webchat.freenode.net/?channels=%2396boards) channel #96boards (there are many ways to access IRC, this website is one of them). Dig around the wiki, create a new forum thread, and/or post a question in the chat.

**Below is the chat log from the OpenHours session today:**

RW

Hello!

RW

[https://www.youtube.com/playlist?list=PL-NF6S9MM_W1QBjUc2B5Pg502bz7qslxk](https://www.youtube.com/playlist?list=PL-NF6S9MM_W1QBjUc2B5Pg502bz7qslxk)

RW

[https://www.youtube.com/playlist?list=PL-NF6S9MM_W1QBjUc2B5Pg502bz7qslxk](https://www.youtube.com/playlist?list=PL-NF6S9MM_W1QBjUc2B5Pg502bz7qslxk)

Y

when openhours will begin?

[connect.linaro.org](http://connect.linaro.org/)

G2

Do we have to sign in somewhere for the dragonboard giveaway?

Got it

I'm new to this board, what does the Amazon SDK allow us to do in particular? Also is there a way to connect to Watson?

J

For the coursera students, is there a list of sensors and/or other accessories we will need?

[https://github.com/ArrowElectronics/aws-iot-device-sdk](https://github.com/ArrowElectronics/aws-iot-device-sdk)

RW

[https://www.96boards.org/product/dragonboard410c/](/product/dragonboard410c/)

RW

[https://discuss.96boards.org/](https://discuss.96boards.org/)

[https://discuss.96boards.org](https://discuss.96boards.org)

RW

[robert.wolff@linaro.org](mailto:robert.wolff@linaro.org)

[https://www.96boards.org/products/mezzanine/](/products/mezzanine/)

G

What are the list of accessories one needs to buy along with the board ?

J

The problem with the mezzanine is where do you find the connectors for the "clips" what is the references? Arrow does supplies these connectors?

J

[http://www.seeedstudio.com/depot/Grove-Starter-Kit-p-709.html](http://www.seeedstudio.com/depot/Grove-Starter-Kit-p-709.html)

S

What is the cost and can it be delivered anywhere?

LK

Hi J. Everything you need including the cables are in the kit

YZ

Yes, they are worldwide distributed

S

Thanks

Guest

I am also interested in the possibility of Yocto Project with dragon board. What is the status of the support as of now?

G2

Let's say I have a multi-million dollar idea, who do I talk to at Qualcomm to get estimates and more info on mass production?

J

dont forget to buy power supply

Accessories Page: [https://www.96boards.org/products/accessories/](/products/accessories/)

T

Is the dragon board sold in west Africa too?

S

Singapore?

Thanks again

M

what is the difference between dragon board and intel edison

YZ

short answer: Dragonboard is better

RW

[https://github.com/Linaro/documentation/blob/master/Reference-Platform/CECommon/OE.md](https://github.com/Linaro/documentation/blob/master/Reference-Platform/CECommon/OE.md)

J

When is the mini series?

Guest

Thanks..

RW

[https://www.96boards.org/product/dragonboard410c/](/product/dragonboard410c/)

J

connectors on the mezzanine? Who can supply them if I want to connect my sensors Any references, can we order a few with the mezzanine?

RW

[https://www.96boards.org/documentation/consumer/dragonboard/dragonboard410c/getting-started/](https://github.com/96boards/documentation/tree/master/consumer/dragonboard/dragonboard410c/getting-started)

LK

Hi Guest27. If you start development for your million dollar idea on 410c, you have a path to production. you can buy all of the parts to build your own boards from [Arrow.com](http://arrow.com/).

G

I have not tried ubuntu/linaro's coursera's 3rd (sensing and actuation from devices)  examples yet...Robertt, would you recommend Debian flashing instead of linaro/ubuntu?

RW

[www.arrow.com](http://www.arrow.com/)

J

Roughly, what are the concerns/considerations for running the dragonbaord from a battery?  Alkaline/Ni-Cd/Lithium?

A

Ditto for Gerardo's question above about Debian vs. Ubuntu.

Have started the class with Ubuntu but it doesn't exactly match the lectures so far.

S

I am interested in operating environments these work in. How hot and how cold an environment can these operate in?

Also, EMF fields/interferance?

Guest 27

G2

That's awesome.

Guest 28

G2

anyones using the HiKey board on 16.06 you should be aware of the need for the work around captured in this post: [https://discuss.96boards.org/t/hikey-unexpected-shutdown-overheating/#post-16874](https://discuss.96boards.org/t/hikey-unexpected-shutdown-overheating/#post-16874)

S

Yes useful.

Guest 27

G2

Great answer

Are there any zigbee modules?

S

Does anyone know if there are there pressure sensors available?

RW

@Gerardo I would recommend Debian over Ubuntu, it is more current

M

think there is a barometric pressure sensor from seeedstudio

YZ

regarding question about zigbee module: [http://learn.linksprite.com/pcduino/use-pcduino8uno-and-96board-as-zigbee-gateway/](http://learn.linksprite.com/pcduino/use-pcduino8uno-and-96board-as-zigbee-gateway/)

G

thanks for the Debian recommendation... if I go to same link/steps/procedure ( in github?) do I get Debian instead?

RW

@ Gerardo Yes

G

thanks Robert

RW

[https://www.96boards.org/documentation/](https://www.96boards.org/documentation/)

[https://www.96boards.org/documentation/consumer/dragonboard/dragonboard410c/downloads/](https://www.96boards.org/documentation/consumer/dragonboard/dragonboard410c/downloads/)

DT

For barometric pressure BMP280 or BME280 modules work well via I2C

(BME280 adds humidity in one module)

{% include image.html path="/assets/images/blog/OpenHours.png" alt="OpenHours Image" class="img-fluid" %}

Click here to join us for [next OpenHours ](/)
