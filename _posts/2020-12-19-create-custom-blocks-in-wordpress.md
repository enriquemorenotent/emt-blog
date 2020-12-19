---
layout: post
title: "How to create custom block for wordpress"
categories: wordpress
image: https://images.unsplash.com/photo-1566207474742-de921626ad0c?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80
---

Gutenberg is the latest editor for Wordpress. It uses "blocks" to edit the content of its pages and posts. These blocks can be any different kind of stuff: Text, buttons, heading, carousels, dropdowns, etc...

To create your custom blocks, go to your "plugins" folder and run this command:

```bash
npx @wordpress/create-block my-custom-block
```

If you do not know what `npx` is, we are talking about the node package manager for Node.js.

This command will create a new plugin folder with all the necessary files wired up and bootstrapped, so that you can start right away to develop your plugin. Just go to your the plugin page inside Wordpress and **make sure to activate the new plugin.**

If you do not know how to develop custom blocks, I recommend that you watch [this great playlist](https://www.youtube.com/watch?v=ZyZ3KQH7rRQ&list=PLriKzYyLb28lHhftzU7Z_DJ32mvLy4KKH) from [Alessandro Castellani](https://www.youtube.com/channel/UCbmBY_XYZqCa2G0XmFA7ZWg) . In these videos he will explain very well the first steps that you can take to start creating your own blocks.,d
