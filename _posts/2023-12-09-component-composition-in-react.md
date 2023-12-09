---
layout: post
title: "Understanding Component Composition in React"
categories: "web development"
image: images/react.png
excerpt: "How to use component composition in React to build reusable components."
---

*Note: This post is inspired on [this George Moller's tweet](https://twitter.com/_georgemoller/status/1733472087614861388). He posts a lot of content about React. I recommend you to follow him on X.*

React's design philosophy emphasizes the creation of small, reusable components that can be combined to create complex interfaces—a principle known as composition. In this post, we'll explore what composition is and how to apply it by building a `Card` component in two different ways.

## What is Composition?

Composition is a foundational concept in React where smaller components are nested within larger ones to build parts of an application's UI. This process is analogous to constructing a machine from individual parts, where each part has a specific function and can be used to assemble different types of machines.

## Benefits of Composition

- **Reusability**: Components can be reused in different contexts within your app, reducing code duplication.
- **Maintainability**: Smaller, well-defined components are easier to maintain and update.
- **Flexibility**: Customizable components make it easier to adapt the UI to changing requirements.

## A Tale of Two Components

We'll examine two different approaches to implementing a `Card` component: the monolithic approach and the compositional approach. The monolithic approach is simpler and more straightforward, while the compositional approach is more flexible and customizable.

### Approach 1: The Monolithic Component

In the monolithic approach, the `Card` component is a single unit with properties passed in as props.

```jsx
// Card.js
import React from 'react';

const Card = ({ img, title, text, primaryButton }) => {
  return (
    <div className="card">
      <img src={img} alt={title} />
      <h2>{title}</h2>
      <p>{text}</p>
      {primaryButton && <button className="primary">Click me</button>}
    </div>
  );
};

export default Card;
```

The usage is straightforward:

```jsx
// App.js
import Card from './Card';

const App = () => {
  return (
    <Card
      img="path_to_image.png"
      title="Card Title"
      text="Card Text"
      primaryButton={true}
    />
  );
};

export default App;
```

### Approach 2: The Compositional Component

In the compositional approach, `Card` is built out of smaller components that are assembled to form the whole.

```jsx
// Card.js
import React from 'react';

const Card = ({ children }) => {
  return <div className="card">{children}</div>;
};

Card.Img = ({ src, alt }) => {
  return <img className="card-img-top" src={src} alt={alt} />;
};

Card.Body = ({ children }) => {
  return <div className="card-body">{children}</div>;
};

Card.Title = ({ children }) => {
  return <h2 className="card-title">{children}</h2>;
};

Card.Text = ({ children }) => {
  return <p className="card-text">{children}</p>;
};

export default Card;
```

This allows for a more customizable usage:

```jsx
// App.js
import Card from './Card';

const App = () => {
  return (
    <Card>
      <Card.Img src="path_to_image.png" alt="Card image" />
      <Card.Body>
        <Card.Title>Card Title</Card.Title>
        <Card.Text>Card Text</Card.Text>
        <button className="btn btn-primary">Go somewhere</button>
      </Card.Body>
    </Card>
  );
};

export default App;
```

## Conclusion

Composition in React allows for the creation of flexible, maintainable UIs. By composing components, you can easily adapt your UI to the needs of your application without rewriting large chunks of code. Whether you choose a monolithic approach for simpler components or a compositional approach for more complex ones, React's flexibility is one of its strongest assets.

Remember, the best approach depends on your specific use case. Happy coding!