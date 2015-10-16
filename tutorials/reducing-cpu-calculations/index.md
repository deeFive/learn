---
layout: tutorial
title: Reducing CPU calculations
weight: 5970
indent: 1
---

This advice is important for scenes with many individual entities.
<h3>Background</h3>
A 3D engine usually wraps one 3D model in one engine scene graph object - Goo Engine calls them entities. After the wrapping, the engine issues one draw call per entity to the graphics card. Because there is a lot of things going on per draw call (enabling and disabling array attributes, binding buffers, uniforms and textures) this can become costly very fast.
<h3>Hidden Surface Determination and Culling</h3>
Some classic approaches to reducing the number of draw calls are listed here <a href="//en.wikipedia.org/wiki/Hidden_surface_determination">Hidden Surface Determination</a>. But since WebGL renders <a href="//www.opengl.org/wiki/Vertex_Attribute">vertex attribute arrays</a> (which are large lists of surfaces for our purposes) all at once many of these algorithms cost more time to execute in JavaScript then they save.

What we need are algorithms that hide entire entities. The name for this task is called <a href="//en.wikipedia.org/wiki/Hidden_surface_determination#Culling_and_Visible_Surface_Determination_.28VSD.29">Culling</a>

Some popular choices for this task include: View Frustum Culling, Contribution culling and Occlusion culling.

Typically most engines support View Frustum Culling automatically. Additionally, Goo Engine also supports Occlusion culling, so those parts are already covered by the engine.
<h3>What can a user do to reduce the number of draw calls?</h3>
The best thing to do is to combine different entities into one entity using something like a <a href="//code.gooengine.com/latest/docs/MeshBuilder.html">MeshBuilder</a> or <a href="//code.gooengine.com/latest/docs/EntityCombiner.html">EntityCombiner</a>.
<h2>MeshBuilder</h2>
The MeshBuilder is a class that takes vertex attribute arrays from different sources and combines them into one vertex attribute array. Here is an example:
<pre><code>var meshBuilder = new MeshBuilder();
var transform = new Transform();

var box1 = new Box(0.3, 1, 1.6);
var box2 = new Box(0.2, 0.15, 0.7);

transform.translation.setd(0, 0, 1.3);
transform.update();
meshBuilder.addMeshData(box1, transform);

transform.translation.setd(0, 0, 0);
transform.update();
meshBuilder.addMeshData(box2, transform);

var meshData = meshBuilder.build()[0];
gooRunner.world.createEntity(meshData, new Material(ShaderLib.simpleLit)).addToWorld();
</code></pre>
The only problem with this approach is that you can only use one diffuse color texture with the resulting mesh. Therefore, the best way to use this is with meshes that use and share the same <a href="//en.wikipedia.org/wiki/Texture_atlas">texture atlas</a>.
A popular tool to generate a texture atlas is the <a href="//www.codeandweb.com/texturepacker">TexturePacker</a> from CodeAndWeb.
And here is a <a href="http://blog.kalio.net/post/31067884387/yet-another-texture-atlas-packer">python script</a> to create a texture atlas.
<h2>EntityCombiner</h2>
To make life a bit easier Goo Engine includes a utility called the EntityCombiner. It traverses the scene graph and finds all entities that share the same material and combines them using the MeshBuilder.

To test the effect you can create a scene with many entities and initialize the GooRunner with the showStats flag:
<pre><code>var gooRunner = new GooRunner({showStats : true});
var material = Material.createMaterial(ShaderLib.simpleLit);
for(var i=0; i&lt;1000; i++) {
    gooRunner.world.createEntity( new Box(1, 1, 1), [1+(i*0.01),1+(i*0.01),1+(i*0.1)], material).addToWorld();
}
</code></pre>
If you run this you should see a stats widget saying that the scene is using 1000 draw calls. Next add this piece of code:
<pre><code>document.addEventListener('keypress', function(){
    new EntityCombiner(gooRunner.world).combine();
}, false);
</code></pre>
If you refresh the scene in your browser you should still see 1000 draw calls, but after pressing any key you should see that it drops down to one and that the frame rate improves dramatically. When testing on a rather old machine it jumps from 27 FPS to a solid 60 FPS.

Keep this approach very much in mind if you create static models and make them share a single texture atlas to benefit from this feature.

Next: <a href="../reducing-cpu-calculations/">Reducing CPU Calculations</a>