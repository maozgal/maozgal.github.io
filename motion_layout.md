author: Gal Maoz
summary: Some MotionLayout Crafts
id: galm_motion_layout
categories: Animations
environments: Android



# Some MotionLayout Crafts

## Introduction
Duration: 1:00


This tutorial will walk you through creating your first MotionLayout steps.

Using MotionLayout, you'll learn the following concepts:

* Basic animation in MotionLayout.

* Different attributes for animations.

* Photos manipulations.

* Swipes.

* Keyframes.

* More Fun :)

Hope you'll enjoy the codelab!

Positive
: Note : MotionLayout is fully declarative. therefore, you will not use any code to build your animations.

The source code for this codelab can be found on [Github](https://github.com/maozgal/MotionLayout).

## Setup Your Environment
Duration: 3:00

In this step, you will download the code for the entire codelab and run a simple example app.

Click the following link to download the source code for this codelab:
  [Download Code Lab sources](https://github.com/maozgal/MotionLayout/archive/master.zip)

*   Unzip the code, and open the project.
*   Run the app <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%203.34.27%20PM.png" width="100">

The app will display a crazy Emoji and two bottons. You should see something like this:

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/master/pics/device-2018-11-27-095241.png" width="250">

Feel free to visit us on GitHub.
The first phase is on the [master](https://github.com/maozgal/MotionLayout/tree/master) branch.

## Basic Animation
Duration: 8:00

The most important thing to understand in ```MotionLayout``` is its structure.

Positioning views in ```MotionLayout``` is divided into two scenarios:

1.  Static views - views you won't animate will use the ```ConstraintLayout``` toolset - as ```MotionLayout``` is a subclass of it.
2.  Dynamic views - you'll declare these views using ```MotionLayout```, without positioning attributes. Positioning them will be done by an external XML file, called Scene.

When you want to animate a view in your ```MotionLayout```, you will delegate its constraints to your scene file.

A scene is basically where you describe the occurrences of your animations.

Each scene is composed of:
*   A start state - on which you will describe the initial state of the dynamic views.
*   An end state - on which you will describe the final state of the dynamic views.
*   A set of attributes describing the occurrences of the animation between the two states.

The system will calculate all of these parameters and handle the animation for you.

To summarize:
<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/monitor/pics/desc.png">

The first thing you'll want to do is to note where is the scene XML.

You'll do that by adding the layoutDescription parameter to the root view, which just points to the file where the animations are being described.

* Go to res -> ```activity_main.xml```, and add the following line into your ```MotionLayout``` root view :

``` xml
    app:layoutDescription="@xml/scene_01"
```

Your view should look as follows:

``` xml
<android.support.constraint.motion.MotionLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/motionLayout_container"
    android:background="#ffffff"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:layoutDescription="@xml/scene_01"
    tools:context=".MainActivity">
```

Next, create a filed called ```scene_01.xml```.

* Create a folder called ```xml``` under res:
<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%206.45.55%20PM.png">

* Create a new file - ```scene_01.xml``` - inside res -> xml.
* Paste the following into your new scene file:
``` xml
    <?xml version="1.0" encoding="utf-8"?>
    <MotionScene
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:motion="http://schemas.android.com/apk/res-auto">

        <Transition
            motion:constraintSetEnd="@+id/end"
            motion:constraintSetStart="@+id/start"
            motion:duration="1000">
        </Transition>

        <ConstraintSet android:id="@+id/start">
        </ConstraintSet>

        <ConstraintSet android:id="@+id/end">
        </ConstraintSet>

    </MotionScene>
```

Explanation:
In order to take control of an animation, you need to define a ```MotionScene```.
MotionScene is the entity describing the animation. in your case, you'll make a transition from point A to point B on the screen, with a duration of 1 second.

Every point is a ```ConstraintSet```.
The animation will start at ```@+id/start```, and end at ```@+id/end```.

* Paste the following content inside ```@+id/start```:
``` xml
    <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent"/>
```


* Paste the following content inside ```@+id/end```:
 ``` xml
 <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent"/>
```

Your ```scene_01.xml``` file should look like this:

``` xml
 <?xml version="1.0" encoding="utf-8"?>
<MotionScene
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@+id/start"
        motion:duration="1000">

    </Transition>


    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent"/>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent"/>
    </ConstraintSet>

</MotionScene>
```


Explanation:
Take a look at the ```<Constraint>``` of the ```@+id/start``` ConstraintSet,

* You define the view on which you want the animation to run(```@+id/main_iv```).
* Next, you define its constraints.
The current constraints are centering the view vertically and attaching it to the left.

The constraints in ```@+id/end``` are the same, with the only difference being the view is attached to the right.

* Go to src -> ```MainActivity.java```.
* Add the following line of code into ```animateToEndButton```'s onClick call back:

``` bash
mMotionLayout.transitionToEnd();
```
* Add the following line of code into ```animateToStartButton```'s onClick call back:

``` bash
mMotionLayout.transitionToStart();
```

Your onClick listeners should look like this:

``` java
    animateToEndButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            mMotionLayout.transitionToEnd();
        }
    });

    animateToStartButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            mMotionLayout.transitionToStart();
        }
    });
```

**Run your app**

Run the app and tap the buttons - the views should animate back and forth, as expected.

## Attributes
Duration: 5:00

Click the following button to download the source code for this chapter:
  [Download Code Lab sources](https://github.com/maozgal/MotionLayout/archive/attributes.zip)

*   Unzip the code and open the project.
*   Run the app <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%203.34.27%20PM.png" width="100">

The app should look like this:

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/attributes_solution/pics/device-2018-11-28-184148.png" width="250">

Pay attention to the following changes:

*   You're using a ```View``` instead of an ```ImageView``` in ```MainActivity.xml```.

``` xml
 <View
        android:id="@+id/main_iv"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:background="@color/colorAccent"
        />
```
*   You have a new scene file : ```scene_02.xml```.
*   You changed the layoutDescription reference to point to ```@xml/scene_02``` :

``` xml
app:layoutDescription="@xml/scene_02"
```
*   In scene_02.xml, you constrain your view to center to the center-bottom at the start, and center-top at the end of the animation.

``` xml
<ConstraintSet android:id="@+id/start">
    <Constraint
        android:id="@+id/main_iv"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:layout_marginBottom="8dp"
        motion:layout_constraintBottom_toTopOf="@+id/animate_to_start_bt"
        motion:layout_constraintStart_toStartOf="parent"
        motion:layout_constraintEnd_toEndOf="parent"/>
</ConstraintSet>

<ConstraintSet android:id="@+id/end">
    <Constraint
        android:id="@+id/main_iv"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:layout_marginTop="8dp"
        motion:layout_constraintStart_toStartOf="parent"
        motion:layout_constraintEnd_toEndOf="parent"
        motion:layout_constraintTop_toTopOf="parent"/>
</ConstraintSet>
```

Give it a shot by playing with the buttons.

Let's go over some attributes that can be changed during the animation.

*   Changing size:
    Change layout_height of the end ```ConstraintSet``` to 164dp

``` xml
android:layout_height="164dp"
```

**Run your app**

*   Alpha :
Add the following attribute to your start ```Constraint```

``` xml
android:alpha="1.0"
```

Add the following attribute to your end ```Constraint```

``` xml
android:alpha="0.5"
```
**Run your app**

*   Rotation :
Add the following attribute to your start ```Constraint```

``` xml
android:rotation="0.0"
```

Add the following attribute to your end ```Constraint```

``` xml
android:rotation="-720"
```
**Run your app**

*   Translation :
Add the following attribute to your start ```Constraint```

``` xml
android:translationX="0dp"
```

Add the following attribute to your end ```Constraint```

``` xml
android:translationX="100dp"
```
**Run your app**

*   Changing color:
    You will need  to add a ```CustomAttribute``` to your ```Constraint```, both the start and the end:

``` xml
<ConstraintSet android:id="@+id/start">
    <Constraint
        android:id="@+id/main_iv"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:layout_marginBottom="8dp"
        motion:layout_constraintBottom_toTopOf="@+id/animate_to_start_bt"
        motion:layout_constraintEnd_toEndOf="parent"
        motion:layout_constraintStart_toStartOf="parent">
        <CustomAttribute
            motion:attributeName="backgroundColor"
            motion:customColorValue="#00ff00" />
    </Constraint>
</ConstraintSet>

<ConstraintSet android:id="@+id/end">
    <Constraint
        android:id="@+id/main_iv"
        android:layout_width="64dp"
        android:layout_height="164dp"
        android:layout_marginTop="8dp"
        motion:layout_constraintEnd_toEndOf="parent"
        motion:layout_constraintStart_toStartOf="parent"
        motion:layout_constraintTop_toTopOf="parent">
        <CustomAttribute
            motion:attributeName="backgroundColor"
            motion:customColorValue="#ff0000" />
    </Constraint>
</ConstraintSet>
```

**Run your app**

## Interpolations
Duration: 1:00

A quick word about interpolations.

You can define an interpolator for every ```<Transition>```.

* Go ahead and try one of the following :

    <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/master/pics/Screen%20Shot%202018-11-29%20at%2010.39.39%20AM.png">

## Photos manipulations

Duration: 5:00

Images have a special set of attributes you're going to try and explore.

Go back to your image view settings :

*   [Download](https://github.com/maozgal/MotionLayout/raw/image_manipulation/app/src/main/res/drawable/icon2.png) this new image and add it to your ```drawable``` folder.

*   Next, use an ```ImageFilterView``` instead of a ```View``` in ```MainActivity.xml```.

``` xml
 <android.support.constraint.utils.ImageFilterView
        android:id="@+id/main_iv"
        android:src="@drawable/icon2"
        android:layout_width="64dp"
        android:layout_height="64dp"/>
```
*   Create a new scene file: ```scene_03.xml```.
*   Change the layoutDescription reference to point to ```@xml/scene_03``` :

``` xml
app:layoutDescription="@xml/scene_03"
```
*   Paste the following into ```scene_03.xml```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<MotionScene
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@+id/start"
        motion:duration="1000">

    </Transition>


    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent">

        </Constraint>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent">

        </Constraint>
    </ConstraintSet>

</MotionScene>
```

You can also checkout the [image_manipulation](https://github.com/maozgal/MotionLayout/archive/image_manipulation.zip) branch.

* Saturation :
    *  In ```scene_03.xml```, add a saturation ```CustomAttribute``` to the start and end ```Constraint```s :

     ``` xml
    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent">
            <CustomAttribute
                motion:attributeName="saturation"
                motion:customFloatValue="1" />
        </Constraint>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent">
            <CustomAttribute
                motion:attributeName="saturation"
                motion:customFloatValue="0" />
        </Constraint>
    </ConstraintSet>
    ```

    **Run your app**

* Contrast :
    *   In ```scene_03.xml```, add a contrast CustomAttribute to the start Constraint :

     ``` xml
    <CustomAttribute
                motion:attributeName="contrast"
                motion:customFloatValue="1" />
    ```

    And your end ```Constraint``` should get:

     ``` xml
    <CustomAttribute
                motion:attributeName="contrast"
                motion:customFloatValue="1" />
    ```

    **Run your app**

* Warmth :
    *   In ```scene_03.xml```, add a warmth CustomAttribute to the start Constraint :

     ``` xml
    <CustomAttribute
                motion:attributeName="warmth"
                motion:customFloatValue="1" />
    ```

    And your end ```Constraint``` should get :

     ``` xml
    <CustomAttribute
                motion:attributeName="warmth"
                motion:customFloatValue="2" />
    ```

    **Run your app**

* Altering an image with a fade :
    *   In ```activity_main.xml```, Add altSrc to your ```ImageFilterView``` :

    ``` xml
    <android.support.constraint.utils.ImageFilterView
        android:id="@+id/main_iv"
        android:src="@drawable/icon2"
        app:altSrc="@drawable/icon"
        android:layout_width="64dp"
        android:layout_height="64dp"/>
    ```

    *   In ```scene_03.xml```, add a crossfade CustomAttribute to the start and the end Constraint :

     ``` xml
    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent">
            <CustomAttribute
                motion:attributeName="crossfade"
                motion:customFloatValue="0" />
        </Constraint>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent">
            <CustomAttribute
                motion:attributeName="crossfade"
                motion:customFloatValue="1" />
        </Constraint>
    </ConstraintSet>
    ```

    **Run your app**

## Swipes
Duration: 4:00

MotionLayout can handle the transition without any callbacks in your code. You can add interactivity by specifying relevant options in your XML scene.
Your user will be able to simply swipe the views back and forth to animate them.
This swipe isn't a simple trigger, but also takes acceleration and velocity into account.

Let's try it now.

*   Get rid of your buttons in ```activity_main.xml``` and remove ```handleViews()``` from ```MainActivity.java```.


``` xml
app:layoutDescription="@xml/scene_04"
```

*   Paste the following into ```scene_04.xml```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<MotionScene
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@+id/start"
        motion:duration="1000">

    </Transition>


    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent">

        </Constraint>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent">

        </Constraint>
    </ConstraintSet>

</MotionScene>
```

*   Your ```activity_main.xml``` should look like:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.motion.MotionLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/motionLayout_container"
    android:background="#ffffff"
    android:layout_width="match_parent"
    app:layoutDescription="@xml/scene_04"
    android:layout_height="match_parent"
    tools:context=".MainActivity">


    <android.support.constraint.utils.ImageFilterView
        android:id="@+id/main_iv"
        android:src="@drawable/icon2"
        android:layout_width="64dp"
        android:layout_height="64dp"/>


</android.support.constraint.motion.MotionLayout>
```

*   Go to your ```scene_04.xml```, and change your ```<Transition>``` into the following :

``` xml
<Transition
    motion:constraintSetEnd="@+id/end"
    motion:constraintSetStart="@+id/start"
    motion:duration="1000">
    <OnSwipe
        motion:touchAnchorId="@+id/main_iv"
        motion:touchAnchorSide="right"
        motion:dragDirection="dragRight" />
</Transition>
```
 **Run your app**

## KeyFrame
Duration: 7:00

Up until now, you defined a pair of ```start``` and ```end``` states, letting ```MotionLayout``` transition between them.
You might ask your self, though - what if I want more than two states?

This is where ```Keyframes``` are powerful.

The main idea of a Keyframes is to give you a way to manipulate the animation in terms of size, color, rotation etc during its transition from the start to end state.

Next, you'll take an ```ImageView``` from bottom to top (centered horizontally), but this time ading a Keyframe that changes the bottom-up linear path into a diagonal path that goes from bottom-end to center-start and then to up-end.

*   Create a new scene file: ```scene_05.xml```.
*   Change the ```layoutDescription``` reference to point to ```@xml/scene_05``` :

``` xml
app:layoutDescription="@xml/scene_05"
```

*   Paste the following into ```scene_05.xml```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<MotionScene
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@+id/start"
        motion:duration="1000">
        <OnSwipe
            motion:touchAnchorId="@+id/main_iv"
            motion:touchAnchorSide="top"
            motion:dragDirection="dragUp"/>
    </Transition>


    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginBottom="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintEnd_toEndOf="parent">

        </Constraint>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginTop="8dp"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent">

        </Constraint>
    </ConstraintSet>

</MotionScene>
```

*   Add the following below ```onSwipe```:

``` xml
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
</KeyFrameSet>
```

**Run your app**

Explanation :
*   ```percentX```: Left of the parent.
*   ```framePosition```: When the action takes place in the timeline.
*   ```target```: The view being affected by the transition.

Let's try a more complicated ```KeyFrameSet```.

*   Replace your ```KeyFrameSet``` with the following :

``` xml
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="25"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="1"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="70"
        motion:target="@id/main_iv"/>
</KeyFrameSet>
```    

**Run your app**

Let's step it up a notch! Aside from ```KeyFrame```s, you also have ```KeyAttribute``` which lets you play around with basic view attributes such as size, color, rotation etc.

Enlarge your view to twice its size and rotate it -45 degrees at the halfway point of your animation:

*   Replace your ```KeyFrameSet``` with the following :

``` xml
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="25"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="1"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="70"
        motion:target="@id/main_iv"/>

    <KeyAttribute
        android:scaleX="2"
        android:scaleY="2"
        android:rotation="-45"
        motion:framePosition="50"
        motion:target="@id/main_iv" />
</KeyFrameSet>
```    

**Run your app**

And if we will go wild :

*   Replace your ```KeyFrameSet``` with the following :

``` xml
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="25"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="1"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="70"
        motion:target="@id/main_iv"/>
    <KeyAttribute
        android:rotation="-45"
        motion:framePosition="25"
        motion:target="@id/main_iv" />
    <KeyAttribute
        android:scaleX="2"
        android:scaleY="2"
        android:rotation="-245"
        motion:framePosition="50"
        motion:target="@id/main_iv" />
    <KeyAttribute
        android:rotation="-445"
        motion:framePosition="75"
        motion:target="@id/main_iv" />
</KeyFrameSet>
```    

**Run your app**

## Cool stuff with KeyFrames
Duration: 3:00

You can leverage keyframes to create some cool combinations.

*   Create a new scene file: ```scene_06.xml```.
*   Change the ```layoutDescription``` reference to point to ```@xml/scene_06``` :

``` xml
app:layoutDescription="@xml/scene_06"
```

*   Paste the following into ```scene_06.xml```:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<MotionScene
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@+id/start"
        motion:duration="1000">

    </Transition>

    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginBottom="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent">

        </Constraint>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginTop="8dp"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent">

        </Constraint>
    </ConstraintSet>

</MotionScene>
```

* Go to ```activity_main.xml``` and add the following lines:

``` xml
<Button
        android:id="@+id/animate_to_start_bt"
        android:layout_width="0dp"
        android:layout_height="50dp"
        android:layout_marginBottom="10dp"
        android:text="Animate To Start"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/animate_to_End_bt"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"/>

    <Button
        android:id="@+id/animate_to_End_bt"
        android:layout_width="0dp"
        android:layout_height="50dp"
        android:layout_marginBottom="10dp"
        android:text="Animate To End"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/animate_to_start_bt"/>
```

Also, in ```activity_main.xml```, add :

``` xml
private void handleViews() {
    animateToEndButton = findViewById(R.id.animate_to_End_bt);
    animateToStartButton = findViewById(R.id.animate_to_start_bt);
    mMotionLayout = findViewById(R.id.motionLayout_container);


    animateToEndButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            mMotionLayout.transitionToEnd();
        }
    });

    animateToStartButton.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            mMotionLayout.transitionToStart();
        }
    });
}
```

And call ```handleViews()``` from ```onCreate()```.

*   Next, add the following lines itno ```<Transition>``` :

``` xml
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentY="0.25"
        motion:percentX="0.75"
        motion:framePosition="25"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentY="0.5"
        motion:percentX="0.1"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentY="0.75"
        motion:percentX="0.75"
        motion:framePosition="75"
        motion:target="@id/main_iv"/>
</KeyFrameSet>
```

You can even go a bit crazier and do the following:

``` xml
<Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@+id/start"
        motion:duration="4000">
        <KeyFrameSet>
            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="0.80"
                motion:percentX="0.80"
                motion:framePosition="2"
                motion:target="@id/main_iv"/>
            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="0.60"
                motion:percentX="0.80"
                motion:framePosition="10"
                motion:target="@id/main_iv"/>
            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="0.70"
                motion:percentX="1"
                motion:framePosition="15"
                motion:target="@id/main_iv"/>
            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="0.80"
                motion:percentX="0.80"
                motion:framePosition="20"
                motion:target="@id/main_iv"/>

            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="0.80"
                motion:percentX="0.20"
                motion:framePosition="25"
                motion:target="@id/main_iv"/>
            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="0.90"
                motion:percentX="0.10"
                motion:framePosition="30"
                motion:target="@id/main_iv"/>
            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="1"
                motion:percentX="0.20"
                motion:framePosition="35"
                motion:target="@id/main_iv"/>


            <KeyPosition
                motion:keyPositionType="parentRelative"
                motion:percentY="0.2"
                motion:percentX="0.20"
                motion:framePosition="40"
                motion:target="@id/main_iv"/>
        </KeyFrameSet>
    </Transition>
```

**Run your app**

## Arcs
Duration: 5:00

MotionLayout offers you the ability to transform a linear path between two points to an arch.

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/arcs/pics/arcs.png" width="500">

*   Create a new scene file: ```scene_07.xml```.
*   Change the ```layoutDescription``` reference to point to ```@xml/scene_07```:

``` xml
app:layoutDescription="@xml/scene_07"
```

*   Paste the following into ```scene_07.xml```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<MotionScene
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@+id/start"
        motion:duration="1000">
        <OnSwipe
            motion:touchAnchorId="@+id/main_iv"
            motion:touchAnchorSide="top"
            motion:dragDirection="dragUp"/>

    </Transition>

    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginBottom="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent">

        </Constraint>
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginTop="8dp"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent"
            motion:layout_constraintBottom_toBottomOf="parent">

        </Constraint>
    </ConstraintSet>

</MotionScene>
```

For this property, you'll want to actually see the path.
* Go to ```activity_main.xml``` and add the following line to the root view :

``` xml
app:showPaths="true"
```

* Go to ```scene_06.xml``` and add to the following line to the child ```<Constraint>``` of  ```<ConstraintSet android:id="@+id/start">``` :

``` xml
motion:pathMotionArc="startHorizontal"
```

You should end up with the following:

``` xml
<ConstraintSet android:id="@+id/start">
    <Constraint
        motion:pathMotionArc="startHorizontal"
        android:id="@+id/main_iv"
        android:layout_width="180dp"
        android:layout_height="180dp"
        android:layout_marginBottom="8dp"
        motion:layout_constraintBottom_toBottomOf="parent"
        motion:layout_constraintEnd_toEndOf="parent">

    </Constraint>
</ConstraintSet>
```

**Run your app**

You can also decide that you want your arch to only run for a portion of the path, and not all of it:

* Delete the following line from your end ```<Constraint>```:

``` xml
motion:layout_constraintStart_toStartOf="parent"
```

* Add the following lines to your ```<Transition>``` :

``` xml
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentY="0.5"
        motion:pathMotionArc="none"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
</KeyFrameSet>
```

**Run your app**

* Change ```pathMotionArc``` to ```flip``` :

``` xml
motion:pathMotionArc="flip"
```

**Run your app**

## Monitor
Duration: 3:00

The last feature you'll play with today is a tool that lets you monitor your animation manually.
You'll pass the control of the animation to a ```Seekbar```. This way, you can understand exactly what is happening in every frame of your scene, in an interactive way.

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/monitor/pics/vid.gif" width="250">

You can control the progress of a ```MotionLayout``` by the ```setProgress()``` method.

*   Get rid of your buttons in ```activity_main.xml```, and add a seekbar instead :

``` xml
<android.support.v7.widget.AppCompatSeekBar
        android:id="@+id/seek"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        android:layout_marginBottom="10dp"/>
```


*   On ```MainActivity.java```, change ```handleViews()``` method to :

``` bash
 private void handleViews() {
    mMotionLayout = findViewById(R.id.motionLayout_container);
    SeekBar seekBar = findViewById(R.id.seek);
    seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
        @Override
        public void onProgressChanged(SeekBar seekBar, int i, boolean b) {
            mMotionLayout.setProgress(i / 100f);
        }

        @Override
        public void onStartTrackingTouch(SeekBar seekBar) {

        }

        @Override
        public void onStopTrackingTouch(SeekBar seekBar) {

        }
    });
}
```

**Run your app**

## Project animation
Duration: 60:00

Now is your turn :)

You are going to build the following animation:


<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/freestyle/pics/anim.gif" width="250">
