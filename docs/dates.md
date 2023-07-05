# Using `Day.js` for Date Manipulation

At wakeflow, we adhere to a consistent approach when it comes to date manipulation in our front-end and back-end development. We utilize the `Day.js` library as our preferred choice for handling date and time operations. In this guide, we'll explore the benefits of `Day.js` and how it ensures consistency across our projects.

## Install
To get started with `styled-components`, you can install it using npm or yarn:
```bash
npm i dayjs
```
or

```bash
yarn add dayjs
```

## Example `Day.js` Function

The following code snippet demonstrates an example of a `Day.js` function that showcases how we can leverage `Day.js` for date manipulation.

```javascript
import dayjs from 'dayjs';

export const formatDate = (date, format = 'YYYY-MM-DD') => {
  return dayjs(date).format(format);
};
```
## Why `Day.js`?

`Day.js` offers several advantages for date manipulation, making it an excellent choice for our projects:

1. **Lightweight:** `Day.js` is a lightweight library that provides a minimalistic and fast alternative to larger date manipulation libraries like Moment.js. It has a small footprint, which improves the performance and load time of our applications.

2. **Simple and Intuitive API:** `Day.js` has a simple and intuitive API, making it easy to work with and understand. Its API is similar to Moment.js, which allows developers familiar with Moment.js to transition seamlessly.

3. **Modularity:** `Day.js` follows a modular architecture, allowing us to import only the specific features we need. This reduces the overall bundle size of our applications, optimizing performance and improving efficiency.

4. **Immutable and Chainable:** `Day.js` uses immutable operations, ensuring that the original date object remains unchanged during manipulation. Additionally, `Day.js` supports method chaining, allowing for concise and readable code.

By adopting `Day.js` for date manipulation, we ensure consistency and efficiency across our projects, enabling smoother collaboration and easier maintenance.

## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

