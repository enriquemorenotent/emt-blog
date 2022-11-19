---
layout: post
title: "Animating an rigged humanoid model in Unity"
categories: unity
image: https://unity.com/logo-unity-web.png
---

First create an empty scene, and add an rigged humanoid model to it. For this example, I am going to be using an model taken from the [Polygon packages](https://syntystore.com/collections/frontpage){:target="_blank"} from Synty.

![](https://i.imgur.com/QLLLaia.png)

Now head to [Mixamo](https://www.mixamo.com/#/){:target="_blank"} and login with your account (make one if you dont have it), and select one of the animations that you want to use. In this case I am going to use the "Hip hip dancing" animation.

![](https://i.imgur.com/b0yBgs1.png)

Press the download button and will download a .fbx file. Move this file inside your Unity Assets folder. Inside Unity, select the FXB file. Now make the following modification in the inspector:
1. In the "Rig" tab, select the "Animation Type" to "Humanoid", then click "Apply".
2. You might have to click on "Configure" and adapts the rig, depending on the anatomy of your model. In my case, I will leave it as it is.
3. Go to the "Animation" tab, and make sure that the "Loop" options is checked and all the "Bake into pose" options are checked. Then click "Apply".

Now all you have to do is create an animation controller, create an empty state and select the assign the animation you just downloaded to it. Then you can play the animation by pressing the play button.

![](https://i.imgur.com/jyLScxW.gif)

Mind that there are many setting all over the place, and many things that can be modified to adapt better to your model and animation. This is just a quick guide to get you started.