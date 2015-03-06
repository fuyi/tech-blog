---
title: "modern web application framework components"
layout: "post"
permalink: "/modern-web-application-framework-components.html"
uuid: "5243263727610741789"
guid: "tag:blogger.com,1999:blog-1883517908930132713.post-5243263727610741789"
date: "2013-03-07 10:06:00"
updated: "2013-03-07 10:06:50"
description: 
blogger:
    siteid: "1883517908930132713"
    postid: "5243263727610741789"
    comments: "0"
categories: 
author: 
    name: "yi fu"
    url: "https://plus.google.com/113933316349893218335?rel=author"
    image: "//lh5.googleusercontent.com/-RY4EcCOpnXk/AAAAAAAAAAI/AAAAAAAALqQ/dv3UX9fj58s/s512-c/photo.jpg"
published: "false"
---

<div class="css-full-post-content js-full-post-content">
<div dir="ltr" style="text-align: left;" trbidi="on"><br /><div class="p1">Abbreviation:In this article, write about components which composes web framework. From very simple ones to advanced ones</div><div class="p2"><br /></div><div class="p1">After working with web projects (web 2.0 application) for a few years, I start to think about creating my own framework. As the preparation, I write down here components which comprise of modern web application framework. these components are irrelevant to business logics and programming language, however, as using scenario varies, some of them are essential for all cases, the others are applicable for same specific cases. So I generally categories all components into 2 categories: essential and extension.&nbsp;</div><div class="p2"><br /></div><div class="p3">Essential Components:</div><div class="p2"><br /></div><div class="p3">1) Routing/ Reverse Routing</div><div class="p3">Routing is the entry point of web framework, it builds map between request url into action. action is a function which receive request, output resonse</div><div class="p2"><br /></div><div class="p3">2) Request</div><div class="p3">Request is the component handle all request data, store them for action processing. it contains url, request data (query data, posted data), request method (ajax, none ajax), http request method (get, post, input, ) and other http request header.</div><div class="p2"><br /></div><div class="p3">3) Response</div><div class="p2"><br /></div><div class="p3">4) Cookie</div><div class="p2"><br /></div><div class="p3">5) Session</div><div class="p2"><br /></div><div class="p3">6) Template</div><div class="p2"><br /></div><div class="p3">7) Logging</div><div class="p2"><br /></div><div class="p3">8) Error reporting</div><div class="p2"><br /></div><div class="p3">Extension Components:</div><div class="p2"><br /></div><div class="p3">1) Database Abstraction, same interface for various databases</div><div class="p2"><br /></div><div class="p3">2) ORM, (Data access object)</div><div class="p2"><br /></div><div class="p3">3) HTML Abstraction</div><div class="p2"><br /></div><div class="p3">4) I18N (Multi-Language support)</div><div class="p2"><br /></div><div class="p3">5) Event System</div><div class="p2"><br /></div><div class="p3">6) Cache</div><div class="p2"><br /></div><div class="p3">7) Authentication</div><div class="p2"><br /></div><div class="p3">8) Sanitization</div><div class="p2"><br /></div><div class="p3">9) Service Vender (API integration)<br /><br />10) public API</div></div>
</div>