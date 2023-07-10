# Wakeflow ChatGPT

You can develop functions for ChatGPT and install them on Wakeflow. You will be paid $0.01 for every time your function is called.

A function is essentially a piece of functionality that can be made available to ChatGPT. ChatGPT itself decides when to make use of the function. For example, if you ask ChatGPT "Show me a Pulp Fiction meme" and it has a function available that is called "getMeme" and has a description like "returns the url of a meme of the theme the user asked for", then it will likely call that function to get the url of a meme and reply with that url. 


## Instructions

Below we outline how you can develop a function that can be made available to ChatGPT. We use the example of getting a meme, but other usecases include:
- sending emails
- looking up a name in an address book
- writing invoices
- and anything else you can come up with...

Here is a schematic of the overall flow required to publish a function on Wakeflow. We describe each step in more detail below.

![Instructions](https://www.wakeflow.io/instructions.png)

To develop a function you need to 
1. Host an application that makes the function and its docs available
2. Register your function with Wakeflow
3. "Install" the function on your WhatsApp number

### 1. Host an application that makes the function and its docs available
     - /docs
     - /function

The docs function tells Wakeflow how to use your function. It is an OpenAPI specification for your /function endpoint. Let's say you're developing a function that returns a meme. Your /docs endpoint might return a json payload like so:

```json
 "name": "getMeme",
  "description": "returns the url of a meme of the theme the user asked for",
  "parameters": {
    "type": "object",
    "properties": { "theme": { "type": "string" } },
    "required": ["theme"],
  },
```

The functions endpoint needs to allow invoking the function. For example, Wakeflow would need to be able to call the function like so:

```
POST https://your.service.com/function
{
  "theme":"Pulp Fiction"
}
```
and get a response payload like so:
```json
{ "meme": "https://i.kym-cdn.com/photos/images/original/002/092/391/2b5" }
```

### 2. Register your function with Wakeflow:

Once your service is deployed, up and running, you can register it with Wakeflow. To do so:

1. Get yourself a token from https://tokens.wakeflow.io

2. Make a POST request to the Wakeflow API, like so:
```
POST https://api.wakeflow.io/functions
Headers: 
  Authorization: Bearer [token]
Body: 
  {
    "docsUrl":"https://your.service.com/getMeme/docs",
    "functionUrl":"https://your.service.com/getMeme/function" 
  }
```
This will return a payload containing the functionId like so:
```json
  { "functionId": "abc123" }
```

### 3. "Install" the function on your WhatsApp number

You can then "install" the function for your personal whatsapp number by making a POST request like so:

```
POST https://api.wakeflow.io/functions/abc123/users
Headers: 
  Authorization: Bearer [token]
Body: 
  { "phone": "+44123456789" }
```
You are now able to test your function end-to-end on WhatsApp by WhatsApping the following number: +44 7451 282218

### Review

We will then review your function and test it. If your function does not 
- throw any errors
- provide offensive content
- show unexpected results for the users

we'll make it universally available for anyone to install in our App Store.


## Help and Support
If you get stuck or need any help. Please don't hesitate to contact us by whatsapping: +447500172268. Any feedback is always welcome.





