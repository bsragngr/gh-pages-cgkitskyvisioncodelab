---
title: "Sample Code"
description: 3
---

**Sample Code**

1. In **InitScene** method, you need to implement the model as follow,

   `String modelName = "models/**space_ship.obj**";`
   
   <pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>// Here the textures is loaded. You need to change location and name of the texture according to your file.
   String texAlbedo = "models/texture/spaceship_texture.png";
   String texNormal = "models/texture/spaceship_texture_normal.png";
   String texEmissive = "shaders/pbr_brdf.png";
   <span class="pln"></span></code></pre>

In here, albedo texture is implemented:

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//Here the method of setting texture to the object.
material->SetTexture(TextureType::TEXTURE_TYPE_ALBEDO, texAlbedo);
<span class="pln"></span></code></pre>

In here, normal texture is implemented:

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//Here the method of setting texture to the object.
material->SetTexture(TextureType::TEXTURE_TYPE_NORMAL, texNormal);
<span class="pln"></span></code></pre>

You can find defined texture types in CG kit, 

[https://developer.huawei.com/consumer/en/doc/HMSCore-References-V5/texturetype-0000001050188024-V5](https://developer.huawei.com/consumer/en/doc/HMSCore-References-V5/texturetype-0000001050188024-V5)

In **CreateSkyBox** method, created cube obj file is used:

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>String modelName = "models/cube/cube.obj";
<span class="pln"></span></code></pre>

To implement skybox in **CreateSkyBox** method, a texture for skybox is used:

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>material->SetTexture(TextureType::TEXTURE_TYPE_ENVIRONMENTMAP, m_envMap);
<span class="pln"></span></code></pre>

“**m_envMap**” is defined in **MainApplication.h** (You need to change name and location according to your file)

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>String m_envMap = "cubemaps/nature_env/cubemap.cub"; 
<span class="pln"></span></code></pre>

Object can be resized with scale value: 

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>const Vector3 SCENE_OBJECT_SCALE = Vector3(3.0f, 3.0f, 3.0f);
<span class="pln"></span></code></pre>

Object location can be relocated with scale value: 

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>const Vector3 SCENE_OBJECT_POSITION = Vector3(0.0f, -1.0f, 40.0f);
<span class="pln"></span></code></pre>

**MainApplication::ProcessInputEvent** is implemented for rotation and zoom in/out processes.

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>// Rotation Implementation
if (fabs(touchPosDeltaX) > 2.f) {
if (touchPosDeltaX > 0.f) {
m_objectRotation -= 2.f * m_deltaTime; // change rotation speed with constant value(2.f)
} else {
m_objectRotation += 2.f * m_deltaTime; // change rotation speed with constant value(2.f)
}
LOGINFO("Set rotation start.");
}
<span class="pln"></span></code></pre>

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>//Zoom-In, zoom-out implementation
if (fabs(touchPosDeltaY) > 3.f) {
if (touchPosDeltaY > 0.f) {
m_objectScale -= 0.75f * m_deltaTime;
} else {
m_objectScale += 0.75f * m_deltaTime;
}
m_objectScale = min(0.75f, max(0.25f, m_objectScale));
LOGINFO("Set scale start.");
}
<span class="pln"></span></code></pre>

The position of eye is settled in the environment:

<pre><div id="copy-button23" class="copy-btn" title="Copy" onclick="copyCode(this.id)"></div><code>const Vector3 EYE_POSITION(0.0f, 10.0f, -1.0f);
cameraObj->SetPosition(EYE_POSITION);
<span class="pln"></span></code></pre>

Rendering object with skybox :

![](C:\Users\b00568925\Desktop\gh-pages-cgkitcodelab\assets\cg12.jpg)