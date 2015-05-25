---
title: "Real-time leaderboard with Reactjs and Firebase"
keywords: "real time web, websocket, reactjs, firebase"
description: "How to implement a real-time score leaderboard using Reactjs and Firebase"
layout: "post"
permalink: "/2015/05/real-time-leaderboard-with-reactjs-and-firebase.html"

---

# Intruduction

Recently, [Reactjs][1] has been talked many times among my colleagues and the feedbacks from them are mostly positive. I start to get intersted in this tiny UI library open sourced by Facebook, How does it work, what are the design concepts behind it and how is it different from angularjs (which we use for our production app). So I decid to have a peek. After playing around for a few days, I think it is time to get my hand dirty and try to reimplement my current product [Sparta][2]'s one feature: Competition Leaderboard.

![Reactjs][reactjs]

# Project requirement

Competitoin Leaderboard has several basic requirements

1. Competition administrator can add new participants to competition
2. Participants can register points/score
3. Leaderboard updates in real-time once new points/score is registered.
4. Rank is decided by points/score and UI is updated to reflect rank change.

# Get the work done

This section 

## Brief introduction of Reactjs and Firebase

### Reactjs

Reactjs is a tiny library with simple API, focusing on building UI layer only, ensuring data is synced with its representation. As it is stated on its home page:

> Reactjs: A javascript library for building user interface

It's main features are:

* UI only:  It helps develpers to manage View layer in MVC pattern (Note: I don't fully agree here, since it also handles user interaction and events). So it is easy to hook up Reactjs into other client side architecture, let Reactjs render UI only.
* Virtual DOM: It frees developers from DOM manipulation, If you are familiar with DOM manipulation libraray like Jquery, you know what I mean :),  so we can focus on implementing business logic.
* Modularity: Reactjs encapsulates UI as components. each component is independent entity and communicates with other components by passing data through 'props'.

### Firebase

[Firebase][3] is a _backendless_ service provider. It provides storage and cross platform APIs to persist client side data to server side without writting any server side code. One great feature they offer is the build-in PubSub model to __sync data change to all connected clients in real time__. This makes implementing real time app like a breeze.

## Tech stack break down

1. Automatically update UI components when their binding data is changed.
2. Persist participants status, score registration to backend.
3. Push data change to all clients connected in real time.

Item 1 is where Reactjs comes to play, while Firebase is the perfect fit for items 2 and 3

## Project setup

This section shows how to set up a Reactjs project development environment step by step, will be written as a separate post and referred here.

## Demo and code

The demo is available [here][4], open 2 pages of this demo, register some score and you will see the other automatically reflect the change in real time.

source code is available at this [Github Repository][5]

# Incomplete comparision with Angularjs1

In general, I have enjoyed playing with Reactjs. Since our production app is built on angularjs v1, I would like to share my experience with both of them. I just touched the surface of Reactjs, but this is what I got so far:

* Angularjs is a full MVC client side _framework_, while Reactjs is a small _library_ concern only about View layer, Angularjs is much heavier than Reactjs. 
* Angularjs, as a whole front end solution, is more opinionated while Reactjs is more flexible, you can combine it with other preferabble libs to form your own client side stack.
* Angulrajs has more concepts to learn, like dependence injection, directive which means it has steeper learning curve; Reactjs is more straight forward, expreienced javascript engineer can get it withen a day or 2.
* The modularized component archtecture introduced by Reactjs is awesome especially the one way data flow concept, it makes UI development easier and funnier. Angularjs directive has similar concept behind it, but the scope inheritance is anti pattern of code encapsulation and modularation.
* I really like the way angularjs inject business logic into DOM. Using directive in template and $compile service to generate final DOM is very developer friendly; On the other side, Reactjs doesn't have a template system so all DOM related logic like loop and judgement needs to be writen in pure javascript or JSX within render function, it is a bit messy to me. I am looking forward to see a template system implemented in Reactjs.
* The strong selling point of Angularjs is '2 way data binding' which is nice to have but not a must, Reactjs's model of manully calling setState method is more performant.

All in all, if you want a compete frontend stack, then you may love Angularjs, if you like simplicity and the freedom to build your own stack, then you will find Reactjs charming.

__Happy coding!__


<!-- images -->
[reactjs]: https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcQh5GVX7grD4FDI85P02g8p2RMF5FJYSN2FFMGWrcPmjbrsB--nNw "reactjs"

<!-- links -->
[1]: https://facebook.github.io/react
[2]: https://www.spartasales.com
[3]: https://www.firebase.com
[4]: https://resplendent-inferno-6893.firebaseapp.com
[5]: https://github.com/fuyi/leaderboard-react