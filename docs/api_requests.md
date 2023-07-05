# Using `Axios` for API Requests

At wakeflow, we follow a consistent approach when it comes to making API requests in both front-end and back-end development. We utilize the `Axios` library as our preferred choice for handling HTTP requests. In this guide, we'll explore why `Axios` is a better alternative to native browser fetch and how it ensures consistency across our projects.


## Install
To get started with `axios`, you can install it using npm or yarn:
```bash
npm i axios
```
or

```bash
yarn add axios
```

## Example `Axios` function
The code snippet showcases an `Axios` API request function where the `axios` library is used to handle the HTTP request. In the event of an error, relevant details such as the response data, error message, status code, and the function name (createMessagebirdContact) are logged to facilitate effective error handling.

```javascript
export const createMessagebirdContact = async data => {
  try {
    const res = await axios({
      method: `POST`,
      url: `https://contacts.messagebird.com/v2/contacts`,
      headers: {
        'Content-Type': `application/json`,
        Authorization: `AccessKey ${process.env.ACCESS_KEY}`,
      },
      data,

    })
    return res.data
  } catch (err) {
      console.log(err.response?.data)
      console.log(err.message)
      console.log(err.response?.status)
      console.log(`createMessagebirdContactError`)
    throw err
  }
}
```

## Why `Axios`?

`Axios` offers several advantages over fetch, making it an ideal choice for our API request needs:

1. **Promises and async/await support:** `Axios` provides a clean and intuitive syntax for handling asynchronous operations, allowing us to write asynchronous code in a more readable and manageable way. It supports promises and async/await, making error handling and response handling simpler.

2. **Cross-browser compatibility:** `Axios` is designed to work consistently across different browsers, ensuring that our API requests function reliably regardless of the user's browser environment. This eliminates the need for polyfills or workarounds to ensure compatibility.

3. **Interceptors and middleware:** `Axios` offers powerful interceptors and middleware functionality, allowing us to intercept and modify requests and responses at various stages of the request lifecycle. This feature is valuable for implementing global error handling, request/response logging, authentication, and other custom logic.

4. **Response transformation:** With `Axios`, we can easily transform response data using interceptors or by specifying a response transformer. This makes it convenient to parse and modify the API response before it reaches the rest of our codebase, ensuring consistent data structures across different endpoints.

5. **Error handling:** `Axios` provides comprehensive error handling capabilities. It automatically rejects promises on non-2xx HTTP status codes, simplifying error detection and handling. Additionally, we can define custom error handling logic, such as retry mechanisms or handling specific error types.

## Front-End and Back-End Consistency

By adopting `Axios` for API requests in both front-end and back-end development, we achieve a consistent approach across our projects. This consistency simplifies code maintenance, reduces the learning curve for new team members, and enables seamless collaboration between front-end and back-end developers.

Whether we are building web applications using frameworks like React or Vue.js on the front end, or developing server-side applications with Node.js on the back end, we can leverage the same `Axios` API to make HTTP requests.

## Conclusion

Using `Axios` for API requests provides us with a robust and consistent solution for handling HTTP communication in our projects. Its advantages over native browser fetch, such as enhanced syntax, cross-browser compatibility, interceptors, and error handling, make it the preferred choice for our team.


## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

