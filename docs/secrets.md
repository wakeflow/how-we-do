# Loading Environment Variables with `dotenv`

At wakeflow, we adopt a standardized approach to loading environment variables in our front-end and back-end development. For managing environment variables, we utilize the `dotenv` package, which offers a simple and efficient solution. In this guide, we'll explore how `dotenv` enables us to load environment variables seamlessly and maintain consistency across our projects.

## Install

To start using `dotenv`, you can install it using npm or yarn:
```bash
npm i dotenv
```
or

```bash
yarn add dotenv
```
## Usage

### Create a `.env` file in the root directory of your project.

Define your environment variables in the `.env` file using the `KEY=VALUE` syntax. For example:

```plaintext
PORT=3000
API_KEY=abcdef123456
```


In Node.js ONLY, import and declare the following in app.js to be able to gain access to access the environment variables. No need to do this in React.js
```javascript
import dotenv from 'dotenv';
dotenv.config();
```
To access enviroment variables in Node.js and React.js use:
```javascript
const apiKey = process.env.API_KEY
```

## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

