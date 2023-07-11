---
layout: post
title:  "Creating sprites"
date:   2023-07-04 00:00:00 +0800
categories: Unity
---

### Introduction

These notes were created based on [Brackeys 2D Animation Tutorial] (https://www.youtube.com/watch?v=hkaysu1Z-N8)

Creating sprites is a multi step process. The main steps are:
1. Create your sprite (artwork)
2. In Unity, create animations from your artwork
3. From your animations, create an animator to manage transitions to and from
different animation clips
4. Write code to control the transitions

### Creating sprite artwork

Use a pixel editor like [pixilart](https://www.pixilart.com/) pr [piskel](https://www.piskelapp.com/) to create your sprite
![Create sprite artwork]({{ site.baseurl }}/assets/images/sprite/sprite-pixil-create.png)

Export your artwork to get a zip file of the frames.
![Export sprite]({{ site.baseurl }}/assets/images/sprite/sprite-pixil-export-zip.png)

Double click the zip file to expand it. Copy one of the frames out to use as a placeholder
for the sprite in Unity.
![Sprite artwork files]({{ site.baseurl }}/assets/images/sprite/sprite-pixil-exports.png)

### Setting up the sprite in Unity

#### Create the folder structure for your assets
In the 'Project' tab, create two new folders in the 'Asset' folder. Create a 'Sprite' folder for
your sprite artwork. Create an 'Animation' folder for the animation clips.
![Unity folder structure]({{ site.baseurl }}/assets/images/sprite/sprite-unity-folders.png)

#### Set up the initial sprite
Add the sprite artwork you created earlier into the 'Sprite' folder. Just drag the files there.
![Unity folder structure]({{ site.baseurl }}/assets/images/sprite/sprite-unity-import.png)

Now drag the sprite placeholder into your scene. You can scale it up if you want to make it bigger.
![Add sprite to scene]({{ site.baseurl }}/assets/images/sprite/sprite-unity-add-sprite-to-scene.png)

#### Create empty animation clip and animator controller
Open the 'Animation' window (Window -> Animation -> Animation).
![Animation window]({{ site.baseurl }}/assets/images/sprite/sprite-unity-view-animation-window.png)

With the 'Animation' window open, select the sprite placeholder. In the 'Animation' window, you'll
see an option to 'Create' an animation clip. Click the 'Create' button.
![Animation window]({{ site.baseurl }}/assets/images/sprite/sprite-unity-create-animation.png)

You'll now be prompted to choose a file location for your new animation. Create the file
in your 'Assets -> Animation' folder
![Animation window]({{ site.baseurl }}/assets/images/sprite/sprite-unity-save-anim-file.png)

Unity will create 2 files in your 'Animation' folder. One is the the **animation clip**, and the other is the **animator controller**. Select the animation clip to see it in the 'Animation' window
![Animation clip]({{ site.baseurl }}/assets/images/sprite/sprite-unity-animation-assets.png)

#### Create the animation clip
Now it's time to add your sprite artwork to the animation clip. First we need to set up the screen
so it's easier to drag the frames into the animation window. Start by dragging your 'Project' tab upward and docking it above the 'Animation' tab. Now drag the slider to the left so you can see all the frames.
![Setup unity to view frames]({{ site.baseurl }}/assets/images/sprite/sprite-unity-setup-for-animation-clip.png)

Now drag the frames into the animation timeline. You can set 'Sample' to 12 to slow
down the animation. You can hit the play button to preview your animation clip.
![Add sprite artwork to animation clip]({{ site.baseurl }}/assets/images/sprite/sprite-unity-add-frames-to-animation.png)

Add this point, you should be able to play the game and see the sprite animating.

#### Add more animation clipes
Create another set of sprite artwork.
![Create next sprite artwork]({{ site.baseurl }}/assets/images/sprite/sprite-pixil-second-animation.png)

Import the artwork into the 'Asset -> Sprite' folder, in the same way you did before.
![Add artwork for next animation clip]({{ site.baseurl }}/assets/images/sprite/sprite-unity-add-next-clip.png)

In the 'Animation' window, click on the drop down for the existing clip, and choose 'Create New Clip'.
If the button is not showing, try saving your work, or restarting Unity. Save your second animation clip
in the Animation folder (same as before).
![Create new animation clip]({{ site.baseurl }}/assets/images/sprite/sprite-unity-add-next-clip.png)

Drag the artwork for the second sprite into the timeline (same as before). Adjust the 'Sample' rate.
Now you should have two animation clips
![Two animation clips]({{ site.baseurl }}/assets/images/sprite/sprite-unity-two-animation-clips.png)

### Using Animator

You have two clips, but only the first one will show when you play the game. You need to set the 
clips up in 'Animator' to be able to transition between clips.
We'll set up the Animator controller to play a second clip when we hit the space bar.

The [Brackeys] (https://www.youtube.com/watch?v=hkaysu1Z-N8) tutorial does an excellent job of
explaining. Please go through it for more info.

#### Open Animator window
Open the Animator window (Window -> Animation -> Animator)
Alternatively, just double click the **animator controller** in 'Assets -> Animation'
![Animator window]({{ site.baseurl }}/assets/images/sprite/sprite-unity-open-animator-window.png)

You'll see the two animation clips you already created. If some of the clips are not there, 
drag them in from the Assets -> Animation folder.
![Clips in Animator]({{ site.baseurl }}/assets/images/sprite/sprite-unity-animator-window.png)

#### Setting up transitions
Now we need to create a transition from 'Any State' to the second clip. This transition is so that
no matter which animation is playing, we can trigger the second animation.
Right click on the second animation and choose 'Make Transition'
![Make animation transition]({{ site.baseurl }}/assets/images/sprite/sprite-unity-make-transition.png)

Create a transition from the second animation to the first animation. This transition is so that
whenever the space baris **not** pressed, the animation can return to the first animation.
![Create second transition]({{ site.baseurl }}/assets/images/sprite/sprite-unity-all-transition.png)

#### Create parameter
Now we create a parameter to control when we trigger the second animation. Make sure you are on the
'Animator -> Parameter' tab. Click on the '+' button and select 'Bool'. Name the parameter (in this
tutorial, it's called 'IsSparkle').
![Create parameter]({{ site.baseurl }}/assets/images/sprite/sprite-unity-add-parameter.png)

#### Add condition to transitions
Now we modify the transitions to respond to the parameter. Click on the transition from 'All State' to 
'sparkle'. Add a new 'Condition'
![Add condition]({{ site.baseurl }}/assets/images/sprite/sprite-unity-transition-add-condition-1.png)

Choose the IsSparkle parameter we created earlier. Set its value to true. This means that when IsSparkle
is true, the **second** animation will play
![Add condition to first transition]({{ site.baseurl }}/assets/images/sprite/sprite-unity-transition-add-condition-2.png)

Click on the transition from the second animation to the first animation. Add a condition, select the 
IsSparkle parameter and set it to false. This means that when IsSparkle is false, the **first** animation
will play.
![Add condition to second transition]({{ site.baseurl }}/assets/images/sprite/sprite-unity-sparkle-to-moon-transition.png)

### Adding code to set the parameter
Now we have the animator set up, we can write code to set the IsSparkle value to trigger the second animation.

Create a script with the following code
{% highlight csharp %}
using UnityEngine;

public class MoonSprite : MonoBehaviour
{
    // In Unity, set this to the animator we created
    public Animator animator;

    // Start is called before the first frame update
    void Start() { }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            animator.SetBool("IsSparkle", true);
        }
        if (Input.GetKeyUp(KeyCode.Space))
        {
            animator.SetBool("IsSparkle", false);
        }
    }
}
{% endhighlight %}

Select the sprite placeholder and click 'Add Component'. Add the script we just created.
![Add script]({{ site.baseurl }}/assets/images/sprite/sprite-unity-add-script.png)

Now drag the 'Animator' to the 'animator' parameter in the script.
![Set Animator parameter of script]({{ site.baseurl }}/assets/images/sprite/sprite-unity-script-set-animator.png)

You should now be able to play the game and see the animation switch when you hit space.
