# Styling Components with `styled-components`

At wakeflow, we follow a consistent approach to styling components in our front-end development. For our styling needs, we rely on the `styled-components` library, which offers a powerful and intuitive solution. In this guide, we'll explore how `styled-components` allows us to create styled components with ease and maintain consistency across our projects.

## Install

To get started with `styled-components`, you can install it using npm or yarn:

```bash
npm i styled-components
```
or

```bash
yarn add styled-components
```


## Example Usage of `styled-components`

The following code snippet demonstrates an example of sorting an array using the `styled-components` package:

```javascript
import styled from 'styled-components';


const App = () => {
  return (
    <div>
      <Button>Click Me</Button>
    </div>
  );
};

const Button = styled.button`
  background-color: #3498db;
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;

  &:hover {
    background-color: #2980b9;
  }
`;

```
# Why styled-components?

When it comes to styling components, `styled-components` offers numerous advantages that make it a valuable choice for our projects. Here are some reasons why we prefer `styled-components`:

1.  **Component-Based Styling**: `styled-components` allows us to define styles directly within our component files, making it a truly component-based approach to styling. This promotes modularity and encapsulation, as each component carries its own styles, eliminating style conflicts and making our codebase more maintainable.

2.  **CSS-in-JS**: With `styled-components`, we can write CSS styles using JavaScript. This eliminates the need for separate CSS files and provides us with the full power of JavaScript to dynamically generate styles based on props or other variables. It also enables us to create reusable style components and effectively manage CSS dependencies.

3.  **Automatic Vendor Prefixing**: `styled-components` automatically handles vendor prefixing for us, ensuring cross-browser compatibility without the need for manual prefixing. This saves us time and effort, as we don't have to worry about writing vendor-specific CSS rules.

4.  **Styled Theming**: `styled-components` comes with built-in support for theming, allowing us to easily define and switch between different themes in our applications. This feature is beneficial when creating applications with multiple themes or supporting dark mode, as it provides a convenient way to manage and apply theme-specific styles.

5.  **Styled API**: The `styled-components` API is intuitive and easy to use. It allows us to create styled components by defining CSS styles using template literals, making it simple to structure and compose styles for our components.

By leveraging the capabilities of `styled-components`, we can create beautiful, maintainable, and themeable components while enjoying the benefits of a component-based and CSS-in-JS approach.

## Questions
If you have any questions about this process, reach out to andi@wakeflow.io

