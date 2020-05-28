# Enchiridion of Product Design

## Progressive Enhancement

### 1. Identify core functionality 

* Define the core functionality e.g. slack - display/send/receive a message [More examples](#progressive-enhancement)

* Define the lowest common denominator a baseline device (e.g. mobile, tablet, desktop, kindle, alexa)

* Define the initial data model and make it visible `<pre>JSON.stringify()</pre>`

* Design basic structure with `<div>`'s and HTML5 sematic blocks for a baseline device

### 2. Make the core functionality available using the SIMPLEST POSSIBLE TECHNOLOGY. 

* Add behavior (scripts, css hover, onclick(), oninput() etc.)

* Add backend (lambda, database, gateway, queues etc.)

### 3. Enhance

* Add layout markup and stylesheeets for structural layout `.container` with breakpoints

* Add presentational stylesheets for a baseline device

* Add presentational stylesheets for other devices

---

## Progressive Enhancement Examples

* Here’s a three-step approach I take to web design: 

1) Identify core functionality. 
2) Make that functionality available using the simplest possible technology. 
3) Enhance!


* **Information Example** Let’s say you’re a news provider. That right there is the core functionality—to provide news. There are many, many other services you could also provide; interactive puzzles, realtime notifications, and more. Valuable as those services are, they’re probably not as important as making sure that people have access to news.

* How can you make the core functionality available using the simplest possible web technology? That would be an HTML file served up at a URL. Even at this early stage it’s possible to overcomplicate things. The HTML could be unnecessarily bloated. The URL could be unnecessarily verbose; hard to share or recall. Now that the news has been marked up with the appropriate HTML elements—articles, headings, paragraphs, lists, and images—it’s time for step three: enhance!

* By default, the news will be presented using the browser’s own stylesheet. It’s legible, but not exactly pleasurable. By applying your own CSS, you can sculpt the content into a more pleasing shape. Whitespace, leading, colour and contrast are all at your disposal. You can even use custom fonts—an enhancement that was impossible on the web for many years.

* For browsers on large-screen devices, you can introduce layout. It might seem odd at first to think of layout as an enhancement, but that’s the lesson of mobile-first responsive design. Consider the content first, then mark it up with a sensible source order, then apply layout declarations within media queries.

* **Communication Example** Applying the three-step process to a news site is relatively straightforward. Catching up with the news is a fairly passive act. To really test this process, we need to apply it to something more interactive. Suppose we were building a social network. The people using our tool need to be able to communicate with one another regardless of where in the world they are. The core functionality is sending and receiving messages.

* Displaying messages in a web browser isn’t difficult. There might be a lot of complexity on the server involving databases, syncing, queueing, and load balancing, but the HTML needed to structure a reverse-chronological list isn’t very different from the HTML needed for a news site.

* Sending a message from the browser to the web server requires HTML that is interactive. That’s where forms come in. In this case, a form with a text input and a submit button should be enough, at least for the basic functionality.

* People can now receive and respond to messages on our social network, no matter what kind of device or browser they are using. Now the trick is to improve the experience without breaking that fundamental activity.

* If we were to leave the site in this HTML-only state, I don’t think we’d be celebrating our company’s IPO anytime soon. To really distinguish our service from the competition, we need that third step in the process: enhance!

* At the very least, we can apply the same logic we used for the news site and style our service. Using CSS we can provide colour, texture, contrast, web fonts, and for larger screens, layout. But let’s not stop with the presentation. Let’s improve the interaction too. 

* Right now this social network has the same kind of page-based interaction as a news site. Every time someone sends a message to the server, the server sends back a whole new page to the browser. We can do better than that. Time for some Ajax. We can intercept the form submission and send the data to the server using Ajax—I like using the word Hijax to describe this kind of Ajax interception. If there’s a response from the server, we can also update part of the current page instead of refreshing the whole page. This would also be a good time to introduce some suitable animation. We can go further. Browsers that support WebSockets can receive messages from the server. People using those browsers could get updates as soon as they’ve been sent. **Not every browser supports this advanced functionality. That’s okay. The core functionality—sending and receiving messages—is still available to everyone.**

* **Web-based Word Processor Example** Identify core functionality. The tautological answer would be “processing words.” Not very helpful. What do people actual do with this software? They write. They share. They edit. Make that functionality available using the simplest possible technology. Looking at our three verbs—writing, sharing, and editing—we get one of them for free just by using URLs: sharing. The other two—writing and editing—require the use of a form. A basic TEXTAREA element can act as the receptacle for the words, sentences, and paragraphs that will make up everything from technical reports to the great American novel. Submitting that content to a web server means it can be saved for later.

* Technically, that’s a web-based word processor, accessible to anyone with a web browser and an internet connection. But the experience is clunky and dull. It would be a shame not to take advantage of some of slicker options available in modern browsers. Enhance! Using JavaScript, the humble TEXTAREA can be replaced with a richer editing interface, detecting each keystroke and applying styling on the fly. Web fonts can make the writing experience more beautiful. Ajax will allow work to be saved to the server almost constantly, without the need for a form submission. WebSockets provide the means for multiple people to work on the same document at the same time.

* If a browser supports some form of local storage, then data can be stored in a client-side database. Flaky network connections or unexpected power outages won’t get in the way of saving that important document. Using Service Workers, web developers can provide instructions on what to do when the browser (or the server) is offline. These are modern browser features that we should be taking full advantage of …once we’ve made sure that we’re providing a basic experience for everyone.

* We’ve looked at some examples of applying the three-step approach to a few products and services—news, social networking, photo sharing, and word processing. You can apply this approach to many more services: making and updating items in a to-do list, managing calendar appointments, looking up directions, making reservations at nearby restaurants. Each one can be built with the same process: Identify core functionality. Make that functionality available using the simplest possible technology. Enhance!

* This can really clarify which content is most important, something that’s important in a mobile-first responsive workflow. Once you’ve established that, make sure that content is sent from the server as HTML (the simplest possible technology). Then, using conditional loading, you could decide to make Ajax requests for supporting content if the screen real-estate is available.

* We can go deeper. We can apply the three-step process at the scale of individual components within a page. “What is the core functionality of this component? How can I make that functionality available using the simplest possible technology? Now how can I enhance it?”

* Site navigation is another discrete component that lends itself well to a sliding scale of enhancements. The core functionality of navigation is to provide links to resources. The simplest—and still the best—technology to enable that is the humble hyperlink. A list of links should do the trick. With that in place, you are now free to enhance it into something really compelling. Off-canvas navigation, progressive disclosure, sliding, swiping, fading, expanding …the sky’s the limit.

**Note:** Websites do not need to look exactly the same in every browser.

> To the organisers of Hypertext ’91, this seemed hopelessly naïve. They didn’t understand that the simplicity of the web was actually its strength.

* It’s worth remembering that building with progressive enhancement doesn’t mean that everything needs to be made available to everyone. Instead it’s the core functionality that counts. If every single feature needed to be available to every browser on every device, that would indeed be an impossibly arduous process. This is why prioritisation is so important. As long as the core functionality is available using the simplest possible technology, you can—with a clear conscience—layer on more advanced features.

* First, just make it work. Second, make it work better. The design manual also explains why: If you build pages with the idea that parts other than HTML are optional, you’ll create a better and stronger web page.

---

## Three Features or Less

* Product reviews are similar in that they focus on the "missing" features. 
* Those missing features are typically available in a variety of unsuccessfull competitng products, which
leads people to erroneously conclude that a successful product would necessarily have even more features.
* More features = better mindset is the reason why so many smart people are bad at product design.

* What is the right approach to new products:

> Pick three key attributes or features, get those things very very right, and then forget about everything else. 

* Those three attributes define the fundamental essense and value of the product -- the rest is noise.

* For example the original iPod was:
  1) small enough to fit in your pocket
  2) had enough storage to hild many hours of music
  3) easy to sync with your Mac
  
* That is, now wireless, no ability to edit playlists on the device, no support for Ogg, nothing but the essentials, well executed
  
* Gmail had similar approach
  1) it was fast
  2) stored all of your email (back when 4MB quotas were the norm)
  3) had an innovative interface based on conversations and search

* The secondary and teriary features were minimal or absent, no rich text composer, address book was implemented in two days and did almost nothing
  
* Other features can be added or improved later on, but if the basic product isn't compelling, adding more features won't save it.

> By focusing on only a feww core features in the first version, you are forced to find the true essense and value of the product.

* If your product needs "everything" in order to be good, then it's probably not very innovative (though it might be a nice upgrade to an exisiting product). 
* Put another way, if your product is great, it doesn`t need to be good.

* If you are creating a new product, what are the three (or fewer) features that will make it so great that you can cut or half-ass everything else? Are you focusing at least 80% of your effort on getting those three things right?
  
**Disclaimer: This advice probably only applies to consumer products (ones where the purcahser is also the user - this includes some business products). For markets that have purchasing processes with long list of feature requirements, you should probably just crank out as many features as possible and not waste time on simplicity or usability.**

[If your product is Great, it doesn't need to be Good. - Source](http://paulbuchheit.blogspot.com/2010/02/if-your-product-is-great-it-doesnt-need.html)
[Progressive Enhancement - Source](https://github.com/tarasowski/enchiridion/blob/master/006_enchiridion-of-html.md)

