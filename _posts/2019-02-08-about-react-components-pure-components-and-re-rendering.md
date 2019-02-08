---
layout: post
title: 'About React components, pure components and re-rendering'
categories: react
---
Let's take a React component, that simply displays a number. This can be written both as a **class component** or as a **function component**.

```
import React from "react";

class Message extends React.Component {
  render = () =>
    <div className="Message">Number: {this.props.number}</div>;
}

export default Message;
```

```
import React from "react";

const FunctionMessage = ({ number }) => {
  return <div className="Function">Number: {number}</div>;
};

export default FunctionMessage;
```

The problem with these 2 components is that if the components using them re-render, they will re-render as well, even if the props are the same.

To avoid this problem, we have **pure components**. These are components that will only re-render if its props change, even if they parent components re-render.

To write a Pure Component as a class component, we use **React.PureComponent**.

```
import React from "react";

class PureMessage extends React.PureComponent {
  render = () => <div className="Message">Number: {this.props.number}</div>;
}

export default PureMessage;
```

If we want to do the same with a function component, we must use **React.memo**.

```
import React, { memo } from "react";

const MemoFunctionMessage = ({ number }) => {
  return <div className="Function">Number: {number}</div>;
};

export default memo(MemoFunctionMessage);
```

These methods will save you rendering, improving the performance of our React applications.

<iframe src="https://codesandbox.io/embed/jpxokl56n9" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>
