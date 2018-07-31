---
layout: post
title: How to replace "live" with "on" in jQuery 1.7+
categories: ''
---
The functions \`bind\` and \`live\` are being deprecated in jQuery 1.7+ in favor of on, but it’s not very clear how their differences reflect on it. As you might know, “bind” attaches event handlers on DOM elements existing at the time of running the instructions, while \`live\` also attaches these handlers to DOM elements added in the future. So how does it work with “on”?
The functions bind and live are being deprecated in jQuery 1.7+ in favor of on, but it’s not very clear how their differences reflect on it. As you might know, \`bind\` attaches event handlers on DOM elements existing at the time of running the instructions, while \`live\` also attaches these handlers to DOM elements added in the future. So how does it work with \`on\`?

```javascript
$(".myClass").on("click", function(){...});
```

This way jQuery will attach the handler only to DOM elements with the class \`myClass\` that already exist in the DOM tree.

```javascript
$(".myClass1").on("click", ".myClass2", function(){...});
```

This way jQuery will attach the handler to all DOM elements with class \`myClass2\` that are descendants of DOM elements with class \`myClass1\` even if they are added in the future.
