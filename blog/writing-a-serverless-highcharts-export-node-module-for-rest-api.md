---
title: "Writing a Serverless Highcharts-Export Node Module for REST API's"
date: "2019-06-10"
---

In today's post, I'm going to share my experience working with the Highcharts Export server.

I'm going to assume that you already know what that is and spare you the explanation of the [Highcharts](https://www.highcharts.com/) library and their [node export server](https://github.com/highcharts/node-export-server).

**Problem:** I didn't want to run the export server on production and send data to it. Instead, I wanted to implement the export server within my REST API that I built with Node/Express.

**Solution:** Write a module for Node that uses the Highcharts export server module that allows me to do 3 things:

1. Call the `initPool()` function (this starts the service workers that handle the operation)
2. Call the `export()` function
3. Call the `killPool()` function (IMPORTANT!!!)

If `killPool()`isn't called, then memory leaks and causes the CPU/server to slow down considerably. This is a bad scenario, and it must be avoided at all costs.

## The Problem Solving Process

Now, I'm going to walk you through the steps that led me to realize that I need to write my own code instead of copying the example from Highcharts and pasting it directly into my code.

First, I installed the node package as intructed by running the following command:  
`npm install highcharts-export-server -g`

Next, I copied the Node module [example](https://github.com/highcharts/node-export-server#using-as-a-nodejs-module ), and pasted it into my Express Router callback function. I wanted to create an API endpoint that allowed me to pass chart data via JSON and then the API would return base64 encoded strings that represent that chart (which I use to create PDF reports)

However, using this code inside the API endpoint function wasn't working as expected (not surprisingly) I tried shuffling things around a bit, but still no luck...

Then, I realized that this example code was just an example, after all. I decided that it would be best to use it as a guide to craft my own solution instead of trying to force a square peg into a circle hole, or a better analogy: running headfirst into a brick wall over and over again. 😉

So I began working on my own implementation, using the example code as a reference.  

One thing that I needed to add was a Promise "wrapper", which worked wonderfully, but one last bug remained. However, my first attempt at least "sort-of" worked and it looked something like this.

_**WARNING:** Do not copy this code, I only included this in the post to demonstrate the evolution of my solution._

As I stated above, this at least worked to create the charts, but there were a few other issues. Most importantly, the `killPool()` function wasn't being called. It was there in the code, but I could tell it wasn't running because by the 20th export or so my computer was whizzing away and with each export taking longer and longer.

Also, my server kept crashing... This was not good! Although the charts were being _"exported"_ as desired, other problems were being created so, naturally, I set out to solve my new problem:

> How can I stop rogue Service Workers from crashing my computer?

I needed to revise my solution so that I could call the `killPool()` function outside of the `exporter.export()` callback function. So, instead of trying to do everything in one function, I separated the desired functionality into three different functions.

1. `initPool()`
2. `export(exportSettings)`
3. `killPool()`

Using this approach, I stopped encountering memory leaks/server crashes. However, there was still an error message that kept appearing about a _possible_ memory leak. `MaxListenersExceededWarning: Possible EventEmitter memory leak detected. 11 exit listeners added. Use emitter.setMaxListeners() to increase limit`

After re-reading the limited available documentation many times over, I finally realized that I simply needed to add `listenToProcessExits` to the configuration object that I pass along to `initPool()` and set the value to `0`.

This stops the error from being thrown, well it's actually just a warning, and as long as you kill the service workers then calling `process.exit()` isn't necessary, at least that's my understanding.

The warning just informs you that exit listeners are being created but there aren't any exits happening, but that's fine because in my case I want to keep the server alive and running `process.exit()` effectively shuts down my rest API server. I looked at the source code in HighCharts, and the `killPool()` function actually points to the `killAll()` function in the PhantomJS module which is imported via HighCharts Export Server.  

Read more about ending the service workers [here](https://www.npmjs.com/package/highcharts-export-server#note-about-processexit-listeners).

This is what my updated module looked like:

So what did I do differently? Well... I added two more functions: one to start the service workers and one to stop them. Only now, I can call those functions outside of the export callback function.

Also, notice how I've passed a config object to the initPool() function. That's because I read in the [documentation](https://github.com/highcharts/node-export-server#worker-count--work-limit) that phantomJS becomes somewhat unstable the more export requests it has historically handled... so, I tried reducing the defaults a little bit and it did end up operating a little more smoothly as opposed to running with the defaults. (Okay, maybe it was placebo effect.. but if you have any issues I'd recommend experimenting with different parameters for the `initPool()` function to see if it changes anything.)

According to the documentation: _"each of the workers has a maximum number of requests it can handle before it restarts itself. This number is 60 by default, and can be tweaked with_`_--workLimit_`_. As with _`_--workers_`_, this number should also be tweaked to fit your use case. "_

Now, let's take a look at this module in action!

As you can see, this is a fairly easy way to implement the `highcharts-export-server` into your REST API without having to keep the server running separately on production just to export charts.

I hope you found this helpful, and if you have any questions or comments feel free to drop a line using the form below!

Helpful Links:

1. [https://www.highcharts.com/](https://www.highcharts.com/)
2. [https://github.com/highcharts/node-export-server](https://github.com/highcharts/node-export-server)
3. [https://github.com/highcharts/node-export-server#using-as-a-nodejs-module](https://github.com/highcharts/node-export-server#using-as-a-nodejs-module)
