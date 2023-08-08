![alt text](https://wakeflow.io/images/wakeflowbg-p-3200.png)


# Wakeflow GPT Documentation
<img src="https://wakeflow.io/wakeflowlogo-only.png" alt="Pulp Fiction Meme" style="width:60px;"/>

## Table of Contents
- [Introduction](#introduction)
- [Using Wakeflow GPT with the Node-Template](#using-wakeflow-gpt-with-the-node-template)
- [Manipulating API Response with Instruction Field](#manipulating-api-response-with-instruction-field)

---

## Introduction
Wakeflow GPT seamlessly integrates with WhatsApp, leveraging the power of GPT to curate a personalized AI assistant tailored for each user. Dive into our comprehensive documentation to explore our template, empowering you to craft custom functions for the AI assistant. Moreover, our guides elucidate how to utilize these functions, enhancing the capabilities and enriching the user experience.

---
## Using Wakeflow GPT with the Node-Template

To get started with our Wakeflow GPT functions, we recommend using our `node-template`. Here's how you can get started:

1. **Clone the Repository**
   Begin by cloning the `node-template` repository from GitHub:
   ```bash
   git clone https://github.com/wakeflow/node-template.git
    ```

Refer to the README file to learn how to utilize the template for crafting your custom functions.

---

## Manipulating API Response with Instruction Field

Wakeflow API responses can be custom-tailored to your needs by providing specific instructions. When calling the API, you can include an `instruction` field in the response to guide the output's structure and content. This can be extremely useful when you want the result to follow a specific format or style.

### How it Works

When the API returns a response, it also looks at the `instruction` field to structure the response as per the guidelines provided. This allows developers to customize the output in a way that best suits their application.

### Example

Consider the `whatCanWakeflowDo` function:

```javascript
export const whatCanWakeflowDo = errorCatcher(async(req,res) => {
  ...
  res.send({
    capabilities: randomCapabilities,
    instruction: `Show the capabilities of Wakeflow in a bullet points and add emojis to make it more fun! Then show an example of how to use one of the capabilities in whatsapp and ask the user if they want to try it out using the exact text shown in the example field in capabilities.`,
  })
})
```

In the above code:

A response is generated that includes the capabilities and instruction fields.
The instruction provides guidance on how the capabilities should be displayed to the end-user.
In practice, given the instruction, the API might return something like:

🚀 Capability 1: Description for Capability 1

🎉 Capability 2: Description for Capability 2

...

