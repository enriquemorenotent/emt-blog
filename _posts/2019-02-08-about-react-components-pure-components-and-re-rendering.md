---
layout: post
title: "About React, pure components and rendering"
categories: react
image: images/react.png
---

Let's take a React component, that simply displays a number. This can be written both as a **class component** or as a **function component**.

```jsx
import React from "react";

class Message extends React.Component {
  render = () => <div className="Message">Number: {this.props.number}</div>;
}

export default Message;
```

```jsx
import React from "react";

const FunctionMessage = ({ number }) => {
  return <div className="Function">Number: {number}</div>;
};

export default FunctionMessage;
```

The problem with these 2 components is that if the components using them re-render, they will re-render as well, even if the props are the same.

To avoid this problem, we have **pure components**. These are components that will only re-render if its props change, even if they parent components re-render.

To write a Pure Component as a class component, we use **React.PureComponent**.

```jsx
import React from "react";

class PureMessage extends React.PureComponent {
  render = () => <div className="Message">Number: {this.props.number}</div>;
}

export default PureMessage;
```

If we want to do the same with a function component, we must use **React.memo**.

```jsx
import React, { memo } from "react";

const MemoFunctionMessage = ({ number }) => {
  return <div className="Function">Number: {number}</div>;
};

export default memo(MemoFunctionMessage);
```

These methods will save you rendering, improving the performance of our React applications.

In this Codesandbox you have a small example of how renders are activated when the parent component updates.

<iframe src="https://codesandbox.io/embed/jpxokl56n9?autoresize=1" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>
