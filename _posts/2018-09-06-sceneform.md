---
layout: post
title: "Sceneform Overview"
description: "Sceneform Overview"
tags: [arcore,android]
categories: [ar]
---

## Add an ArFragment

The Sceneform API includes ArFragment, which can be added to an Android layout file, like any Android Fragment. For example, here is activity_ux.xml:

{% highlight html %}
{% raw %}
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.google.ar.sceneform.samples.hellosceneform.HelloSceneformActivity">
  <fragment android:name="com.google.ar.sceneform.ux.ArFragment"
      android:id="@+id/ux_fragment"
      android:layout_width="match_parent"
      android:layout_height="match_parent" />
</FrameLayout>
{% endraw %}
{% endhighlight %}

When the activity is launched and the layout is inflated, the fragment automatically performs some required checks:

* It checks whether a compatible version of ARCore is installed and prompts the user to install or update as necessary.
* It checks whether the app has access to the camera and asks the user for permission if it has not yet been granted.

Once complete, the fragment creates an ArSceneView (accessible via getArSceneView() and an ARCore Session.

Note: If you don't want the fragment to do this automatically, perhaps because your app needs to request additional permissions, you can use ArSceneView directly, as demonstrated in the Sceneform solarsystem sample app. You'll need to perform runtime checks, request permissions, create the AR session, and call setupSession() yourself.

The ArSceneView renders the camera images from the session on to its surface. It also highlights Planes (with the default PlaneRenderer) when they are detected by ARCore and in front of the camera.

## Create a renderable

A Renderable is a 3D model, consisting of meshes, materials, and textures, that can be rendered on the screen by Sceneform.

Sceneform provides three ways to create Renderables: from standard Android widgets, from basic shapes/materials, and from 3D asset files (OBJ, FBX, glTF).

The sample app creates a renderable from a 3D andy.obj asset file.

The root build.gradle lists the Sceneform plugin dependency:

{% raw %}
    buildscript {
        …
        dependencies {
            …
            classpath 'com.google.ar.sceneform:plugin:1.4.0'
        }
    }
{% endraw %}

The app build.gradle includes two Sceneform dependencies, applies the plugin and includes a rule for converting the sampledata assets into a resource that is packaged with your app, and that Sceneform can load at runtime:

