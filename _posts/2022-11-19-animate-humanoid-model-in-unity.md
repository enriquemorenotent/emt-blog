---
layout: post
title: "Animating a Rigged Humanoid Model in Unity"
categories: Unity
image: https://unity.com/logo-unity-web.png
excerpt: "In this tutorial, we will delve into the intricacies of animating a humanoid model in Unity."
---

To animate a rigged humanoid model in Unity, begin by creating an empty scene, and adding a rigged humanoid model to it. For the purposes of this tutorial, we will use a model from the [Polygon packages](https://syntystore.com/collections/frontpage){:target="_blank"} provided by Synty.

![Rigged Humanoid Model](https://i.imgur.com/QLLLaia.png)

Next, visit [Mixamo](https://www.mixamo.com/#/){:target="_blank"} and login to your account. If you don't have one already, create one. Select one of the animations that you want to use, for example, "Hip hip dancing" animation.

![Hip Hop Dancing Animation](https://i.imgur.com/b0yBgs1.png)

After selecting your preferred animation, click the download button. A .fbx file will be downloaded, move this file to your Unity Assets folder. In Unity, select the .fbx file, and make the following changes in the inspector:

1. In the "Rig" tab, select the "Animation Type" as "Humanoid", and click "Apply".
2. Click on "Configure", and adjust the rig based on the anatomy of your model. If the rig is already in sync, leave it as it is.
3. In the "Animation" tab, ensure that the "Loop" option is selected, and all the "Bake into pose" options are checked. Then, click "Apply".

Now, all that's left to do is create an animation controller, create an empty state, and assign the downloaded animation to it. You can then play the animation by pressing the play button.

![Animated Humanoid Model](https://i.imgur.com/jyLScxW.gif)

It is worth noting that there are numerous settings scattered throughout Unity, and many adjustments that can be made to better adapt to your model and animation. This tutorial serves as a quick guide to help you get started.
