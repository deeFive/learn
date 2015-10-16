---
layout: tutorial
title: Creating Santa (Christmas Special)
weight: 5600
indent: 1
---

Create comes with a Christmas template project. In this game scene, Santa is traveling around the world with his loyal jetpack. Use the Left and Right keys to accelerate/decelerate and the Up and Down keys to fly higher or lower. This tutorial presents how Santa has been built for this scene and goes through some special Christmas features added in Goo Create.

## It’s All About Primitives

This Mozilla and Goo Christmas challenge was a large competition based around the use of simple shapes to build the worlds. To create a <em>primitive</em>, click on the <em>Create</em> menu at the top of the screen. The following 3d primitives are available:

<img class="wp-image-922 size-full" src="primitives.jpg" alt="" /> All the primitives you need!
<p>Click on the sphere icon to create one in the viewport. A sphere is a perfect start for our Santa Claus, we will use it to build his chest. With the sphere selected, in the left panel, click on the <em>Geometry</em> category, to view the <em>Shape Options</em>:</p>


<img class="size-full wp-image-558" src="image_11.png" alt="Picture of shape options" /> Picture of shape options
<p>Use the sliders to increase or decrease the amount of samples in your sphere in both the X and Y direction. The more samples, the smoother the surface.</p>

<h2>Should Santa Be Red or Green?</h2>
<p>Below the <em>Shape Options</em>, if you click on the <em>Materials</em> category, you can see that Goo Create already created an empty material for you. In the Materials, <em>color (diffuse)</em> section, click on the colored square. A color picker will appear and you'll be able to change the color of your entity.</p>


<a href="image_21.png"><img class="wp-image-559 size-full" src="image_21.png" alt="image_2" /></a> Material panel : Color (diffuse)
<p>Under the color slot you might have noticed a <em>Drop Texture</em> placeholder. If you want to add any texture to your entity just drag and drop an image file from your desktop or from your project library.</p>

<h2>Limb by Limb</h2>
<p>Once you've created your first primitive, practice some more by going through the following construction map using the other primitive shapes available:</p>


<a href="image_3.jpg"><img class="size-full wp-image-560" src="image_3.jpg" alt="Assembly picture" /></a> Assembly picture
<h3>Grouping</h3>
<p>All these limbs can be tiresome to manipulate, and that's when <em>grouping</em> becomes very handy. You can create an empty entity object by clicking on the following icon in the Create panel. It's a bit further down from the primitives!</p>


<a href="image_41.png"><img class="wp-image-923 size-full" src="empty.jpg" alt="" /></a> Create an empty entity
<p>In the project library, drag and drop all the primitives you created on the new entity. You'll then get a complete Santa that can be moved around.</p>


<a href="image_51.png"><img class="size-full wp-image-562" src="image_51.png" alt="Parent an entity to another" /></a> Parent an entity to another
<h2>This jetpack needs some smoke!</h2>
<p><em>Fire</em> and <em>smoke</em> are actions handled through one of Create's secret weapons: the <a title="The State Machine" href="http://goolabs.wpengine.com/learn/the-state-machine/" target="_blank"><em>state machine</em></a>. Click on one entity that should be our smoke emitter (in this case a cylinder located at the bottom of Santa's jetpack). Next, click the <strong>Add Component</strong> button at the top left of the screen. It is located to the right of the entity's name. In the Add Component drop down menu, choose <em>State Machine</em>. Click the <em>State Machine</em> panel to see its options. In the default state (called simply <em>State</em>), click Add Action, then choose <em>Smoke FX</em> in the library.</p>


<a href="image_61.png"><img class="wp-image-924 size-full" src="add-action.jpg" alt="" /></a> Add an action to a state
<p>Now simply press the play button at the bottom of the screen to see smoke coming out of your jetpack. For more information regarding the state machine, take a look at our tutorial <a title="Creating a Goon" href="http://goolabs.wpengine.com/learn/creating-a-goon/" target="_blank">Create a Goon</a> or the article <a title="The State Machine" href="http://goolabs.wpengine.com/learn/the-state-machine/" target="_blank">The State Machine</a>.</p>

<h2>So.. Where Is the Snow?</h2>
<p>If you select the root 'Scene' in the hierarchy on the right panel, <em>Post Effects</em> and <em>Environment</em> should appear inside the left panel. Expand the <em>Environment</em> panel, and you will see the snow effect we've added for the occasion. You may need to place a check mark in the box next to 'Snow' to access the effects properties.</p>


<a href="image_71.png"><img class="size-full wp-image-564" src="image_71.png" alt="Snow options in the environment panel" /></a> Snow options in the environment panel
<p><em>Velocity</em> and <em>rate</em> are quite self-explanatory. <em>Height</em> refers to the distance from the camera's current position.</p>
<p>Now add some snow to your scene to create that special holiday feeling!</p>