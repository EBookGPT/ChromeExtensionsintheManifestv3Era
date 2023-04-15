# Chapter 7: Content Scripts and Message Passing

In the previous chapter, we learned about creating user interface elements and options pages for our Chrome Extension. Now, it's time to dive into the world of content scripts and message passing.

Content scripts allow our extension to interact with the content of web pages. This means we can manipulate the DOM, modify the appearance of a webpage, or even inject new HTML, CSS, or JavaScript. However, content scripts have limited access to the extension's APIs and cannot access the JavaScript of the page itself.

To overcome this limitation, we'll use message passing. Message passing allows our extension to communicate with our content scripts and vice versa. This means we can send messages and data between the background script, content script, and popup.

In this chapter, we'll explore how we can use message passing to execute scripts on webpages, access and modify the DOM, and even retrieve data from APIs. We'll also examine the security implications of using content scripts and message passing, and the potential impact of Manifest v3 changes on their usage.

So buckle up, and let's dive into the world of content scripts and message passing in the Manifest v3 era.
# The Tale of Hermes: A Story of Content Scripts and Message Passing

Once upon a time, in the great kingdom of Browseria, there was a clever god named Hermes. Hermes was known for his speed and cunning, and he was always looking for ways to make browsing the internet faster and more enjoyable.

One day, the people of Browseria came to Hermes with a request. They wanted to be able to quickly access information about the products they were browsing, without having to leave the webpage they were on. Hermes knew just what to do.

He summoned his trusted messengers, the content scripts. These scripts could travel from the extension to the webpage, and back again, carrying messages and data with them. With their help, Hermes was able to create an extension that could inject product information onto the webpage, without the user ever having to leave.

But Hermes knew that content scripts had their limitations. They could manipulate the DOM, but they couldn't access the webpage's JavaScript. To overcome this, he summoned the power of message passing. With message passing, the content scripts could communicate with the extension's APIs, and receive the data they needed to display product information on the webpage.

However, Hermes knew that message passing came with its own risks. Just as he was the messenger of the gods, message passing could also be exploited by malicious actors. He had to be careful not to allow untrusted scripts to access his extension's APIs, or they could potentially steal valuable user data.

As Hermes continued to refine his extension using content scripts and message passing, word spread throughout Browseria of his clever solution to the people's problem. Soon, other gods began to look to Hermes for advice on how to use content scripts and message passing to improve their own extensions and make browsing the internet even more enjoyable for their followers.

And so, thanks to Hermes' ingenuity and the power of content scripts and message passing, browsing the internet in the kingdom of Browseria became faster, more efficient, and more enjoyable than ever before.

#### *Code Sample*
```javascript
// Sending a Message from Content Script to Background Script

// In content script.js
chrome.runtime.sendMessage({greeting: "Hello from content script!"}, function(response) {
 console.log(response.farewell);
});

// In background.js
chrome.runtime.onMessage.addListener(function(request, sender, sendResponse) {
 if (request.greeting === "Hello from content script!") {
   sendResponse({farewell: "Goodbye from background script!"});
 }
});
```
In the Greek Mythology epic, we saw how Hermes used the power of content scripts and message passing to solve a problem for the people of Browseria. Now, let's take a closer look at the code that made it all possible.

The code sample provided demonstrates how to use `chrome.runtime.sendMessage` to send a message from a content script to a background script, and how to use `chrome.runtime.onMessage` to receive that message in the background script and send a response back.

In the content script, we pass an object with a `greeting` property and a callback function as arguments to `chrome.runtime.sendMessage`. The callback function will be called with a `response` object as soon as the message has been successfully sent. This `response` object contains the `farewell` property, which we log to the console.

In the background script, we use `chrome.runtime.onMessage.addListener` to listen for the message from the content script. When we receive the message, we check to see if it has a `greeting` property with the value "Hello from content script!". If it does, we send a `response` object back to the content script, with a `farewell` property and a value of "Goodbye from background script!".

This is a simple example of how we can use message passing between content scripts and background scripts to automate tasks and improve the browsing experience for users. By using the power of message passing and content scripts, we can build extensions that can interact with web pages, modify their behavior, and even send and receive data between the web page and the extension.


[Next Chapter](08_Chapter08.md)