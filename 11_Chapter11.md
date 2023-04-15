# Chapter 11: The Legends of Native Messaging and Native Hosts

Greetings, dear reader! In our previous chapter, we explored the ins and outs of background scripts and events in Chrome extensions. But, that's not all! There's more to know about the power of extensions in the Manifest v3 era. And, today we invite a special guest, Kenji Baheux, a well-known Chrome developer who has been working on improving the platform since the early days of Chrome.

In this chapter, we will discuss Native Messaging and Native Hosts, two powerful capabilities that allow for communication between Chrome extensions and native applications installed on the user's machine. With these features, our extensions can do a wide range of tasks that would have been impossible otherwise. 

As always, we will present several interesting scenarios where extensions can leverage Native messaging to deliver delightful user experiences. While we are at it, Kenji will grace us with his extensive knowledge on the topic, sharing tips and best practices.

So, buckle up for another epic chapter where we journey through the myths of Native Messaging and Native Hosts, and how they can be utilized in Chrome extensions.

But first, let's set some context. Native messaging is not a new capability, in fact, it has been available since Chrome 21! However, in the Manifest v3 era, these capabilities have been extended to allow for more secure and streamlined communication.

As Kenji mentions in his article [Native Messaging: How to build a Chrome Extension that communicates with a Native Application](https://kba.github.io/how-to-build-a-chrome-extension-that-communicates-with-a-native-application/), "In essence, Native Messaging lets a Chrome Extension send and receive messages to or from an application running on the user’s computer". 

Later on, we will explore the mechanics of this communication and go through the step-by-step guide on how to set up Native Hosts, but before that, let's talk about some of the use-cases where Native Messaging can be utilized.

Are you ready? Let's dive in!
# Chapter 11: The Legends of Native Messaging and Native Hosts

The gods of Mount Olympus had watched as Chrome grew and evolved with each passing year. They marveled at the vast array of powerful extensions that mortals had created, granting them abilities to do things beyond their wildest dreams.

One day, as Athena, the goddess of wisdom, was wandering through the mortal realm, she noticed something peculiar. A small group of mortals were huddled together, discussing a powerful new capability that had been bestowed upon Chrome extensions - Native Messaging and Native Hosts.

Curious, Athena approached them and inquired about what they knew of the legends surrounding Native Messaging. A wise mortal by the name of Kenji Baheux stepped forward, and began to teach Athena the many intricacies of this powerful capability.

"Native Messaging," Kenji explained, "is a powerful communication channel between Chrome extensions and native applications installed on the user's machine."

Athena was intrigued and asked what benefits this would bring to the user. Kenji replied, "With Native Messaging, extensions can do tasks that would have been impossible otherwise, like accessing resources that are not available on the web, or interfacing with hardware components."

Athena nodded her head in understanding, but as a goddess, she was baffled by the sheer complexity of what Kenji described. "Surely, such powerful capabilities come with risks," she mused.

Kenji smiled and continued, "Indeed, the power of Native Messaging comes with responsibility to ensure that it is secure and that communication channels are controlled appropriately. With Manifest v3, Google has introduced several changes to make the technology more secure - like requiring message routing through an instance of a native messaging host executable that’s registered with Chrome."

Athena was pleased to hear that powerful technology was also being designed with the users' safety in mind. She was grateful for Kenji's guidance and was glad to hear his advice on how to effectively use this powerful capability.

As she ascended back up to Mount Olympus, Athena could not help but ruminate on the smaller-scale gods and mortals down below. She thought of how much more they will be empowered with this powerful communication technology that Kenji had explained, and how much more they will be able to achieve with it, bringing science and spirituality together.

Though it was a challenging journey, she was glad to have learned of this new avenue that was now available to the Chrome extensions. In a world where the line between human and machine was blurring, she knew the world was one step closer to a more glorious age.
To bring the epic chapter of Native Messaging and Native Hosts to life, we will need to delve into some code! 

First things first, let's break down the main components involved in Native Messaging:

1. **A Native Host Application:** This is an executable program installed on the user's system, which can accept and respond to messages from a Chrome Extension using standard input and output channels. The native host application must be registered manually by the user or with an installer, which can be a script or a package manager.

2. **A Chrome Extension:** This is the JavaScript code that runs in the browser as an extension, and communicates with the Native Host application via message passing using the chrome.runtime.sendNativeMessage function. The manifest.json file for the extension must include a "nativeMessaging" section, specifying the name and location of the native host.

Here's what a typical manifest.json file looks like for a Chrome Extension including a "nativeMessaging" section:

```
{
  "name": "My Awesome Extension",
  "version": "1.0.0",
  "manifest_version": 3,
  "description": "This is my awesome Chrome Extension!",
  "background": {
    "service_worker": "background.js",
    "type": "module"
  },
  "permissions": [
    "nativeMessaging"
  ],
  "nativeMessaging": {
    "name": "com.example.native.host",
    "allowed_origins": [
      "https://www.example.com"
    ]
  }
}
```

The "name" field of the "nativeMessaging" section must match the application name specified in the native host manifest.

Here's an example of how the Chrome Extension can send messages to the Native Host application:

```javascript
const nativePort = chrome.runtime.connectNative('com.example.native.host');
nativePort.postMessage({ 'message': 'Hello from the extension!' });
nativePort.onMessage.addListener((message) => {
  console.log(`Received message from native application: ${message.response}`);
});
```

In this example, we establish a connection to the native host application using the "connectNative" method of the chrome.runtime API, and then send a message via the "postMessage" method. We also register a listener to handle messages received from the native host via the "addListener" method.

On the native host side, here's an example of how to respond to messages from the Chrome Extension:

```python
import json
import sys

def main():
    while True:
        message_len = sys.stdin.buffer.read(4)
        if not message_len:
            sys.exit(0)
        message_len = int.from_bytes(message_len, byteorder='little')
        message = json.loads(sys.stdin.buffer.read(message_len))
        response = {'response': 'Hello from the native host!'}
        sys.stdout.buffer.write(len(json.dumps(response)).to_bytes(4, byteorder='little'))
        sys.stdout.write(json.dumps(response))
        sys.stdout.flush()

if __name__ == '__main__':
    main()
```

In this example, we read messages from the Chrome Extension via standard input, and send responses via standard output. We use Python's "json" module to encode and decode JSON messages.

And that's how the magic of Native Messaging and Native Hosts works! With this powerful capability, extensions can leverage native applications and perform tasks that would have otherwise been impossible or difficult.


[Next Chapter](12_Chapter12.md)