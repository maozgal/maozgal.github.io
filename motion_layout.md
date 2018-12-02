author: Gal Maoz
summary: Some MotionLayout Crafts
id: galm_motion_layout
categories: Animations
environments: Android



# Some MotionLayout Crafts

## Introduction
Duration: 0:05


This tutorial will walk you through the way of creating your first  MotionLayout steps. In this tutorial you will do the following, using MotionLayout:

* Basic animation consepts in MotionLayout.

* Explore the different attributes for animations.

* Explore Photos monipulations in MotionLayout.

* Swipes

* KeyFrames

* More Fun :)

Hope you will enjoy the codelab.

Positive
: Note : MotionLayout is fully declarative. therefore, we will not use any code for animate.

The source code for the codelab is on [Github](https://github.com/maozgal/MotionLayout).



## Setup Your Environment
Duration: 0:10

In this step, you will download the code for the entire codelab and then run a simple example app.

Click the following button to download the source code for this codelab:
  [Download SDK](https://github.com/maozgal/MotionLayout/archive/master.zip)

*   Unzip the code, and then open the project.
*   Run the app <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%203.34.27%20PM.png" width="100">

The app will display a crazy Emoji and two bottons. you should see something like this:

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/master/pics/device-2018-11-27-095241.png" width="250">

Feel free to visit us on GitHub. 
The first phase is on the [master](https://github.com/maozgal/MotionLayout/tree/master) branch
The whole solution can be found on solution branch for each of the chapters

 

## Basic Animation
Duration: 0:10

The most important this to understand in ```MotionLayout``` is the structure.

When you want to animate a view in your ```MotionLayout```, you will delegate its constraints to another XML.
This other XML is your scene.
A scene is basically the place where you describe the occurrences of your animations.
It composites of a start state, an end state and all the movements between them.

The first thing we want to do is to note where is the scene XML.

This is being done by adding layoutDescription parameter to the root view, which just points to the file where the animations are being described.

* Go to res -> ```activity_main.xml```, and add the following line into your ```MotionLayout``` root view : 



``` bash
    app:layoutDescription="@xml/scene_01"
```

The view should be looking new like this : 

``` bash
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

Next step is to create the ```scene_01.xml``` file.
* Create ```xml``` folder under res:
<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%206.45.55%20PM.png">

* Create ```scene_01.xml``` file inside res -> xml.
* Copy the following content inside your ```scene_01.xml``` file:
``` bash
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
In order to take control of an animation, we need to define a ```MotionScene```.
MotionScene is describing the animation. in our case, we will make a transition from point A to point B on the screen, with a duration of 1 second.
 
Each point is a ```ConstraintSet```.
The animation will start at ```@+id/start```, and end at ```@+id/start```.
 
* Copy the following content inside ```@+id/start```:
``` bash
    <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent"/>
``` 


* Copy the following content inside ```@+id/end```:
 ``` bash
 <Constraint
            android:id="@+id/main_iv"
            android:layout_width="180dp"
            android:layout_height="180dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent"/>
``` 

your ```scene_01.xml``` file should look like:

``` bash
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
Take a look at the ```<Constraint>``` of ```@+id/start``` ConstraintSet,
* We define the view on which we want the animation to be affected(```@+id/main_iv```).
* Next, we will define its constraints. These constraints will be affected immediately, as a start stage. 
The current constraints are centering the view vertically and attach it to the left.

The constraints in ```@+id/end``` are the same. only difference is attaching the view to the right.

* Go to src -> ```MainActivity.java```.
* Add the following line of code into animateToEndButton's onClick call back:

``` bash
mMotionLayout.transitionToEnd();
```
* Add the following line of code into animateToStartButton's onClick call back:

``` bash
mMotionLayout.transitionToStart();
```

This should look like:
``` bash
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

**Try up your app now.**

You should be able to animate the view back and forth by clicking the buttons.



## Attributes
Duration: 0:10

Click the following button to download the source code for this codelab:
  [Download SDK](https://github.com/maozgal/MotionLayout/archive/attributes.zip)

*   Unzip the code, and then open the project.
*   Run the app <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%203.34.27%20PM.png" width="100">

The app should be looking like this:

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/attributes_solution/pics/device-2018-11-28-184148.png" width="250">


Pay attention to the following changes.

*   We are using a ```View``` instead of an ```ImageView``` in ```MainActivity.xml```.

``` bash
 <View
        android:id="@+id/main_iv"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:background="@color/colorAccent"
        />
```
*   We created a new scene file : scene_02.xml.
*   We changed the reference layoutDescription to point on @xml/scene_02 : 

``` bash
app:layoutDescription="@xml/scene_02"
```
*   In scene_02.xml we constrained our view to center horizontal + bottom at the start, and center horizontal + top at the end of the animation.

``` bash
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


We will go over some attributes that can be changed during the animation.

*   Changing size: 
    Change layout_height of the end ```ConstraintSet``` to 164dp

``` bash
android:layout_height="164dp"
```

**Try up your app now.**

*   Alpha :
    *   Add the following ```CustomAttribute``` into your start ```Constraint```

        ``` bash
        android:alpha="1.0"
        ```
    
    *   Add the following ```CustomAttribute``` into your end ```Constraint```

        ``` bash
        android:alpha="0.5"
        ```
**Try up your app now.**

*   Rotation :
    *   Add the following ```CustomAttribute``` into your start ```Constraint```

        ``` bash
        android:rotation="0.0"
        ```
    
    *   Add the following ```CustomAttribute``` into your end ```Constraint```

        ``` bash
        android:rotation="-720"
        ```
**Try up your app now.**

*   Translation :
    *   Add the following ```CustomAttribute``` into your start ```Constraint```

        ``` bash
        android:translationX="0dp"
        ```
    
    *   Add the following ```CustomAttribute``` into your end ```Constraint```

        ``` bash
        android:translationX="100dp"
        ```
**Try up your app now.**

*   Changing color:
    You will need  to add a ```CustomAttribute``` into your ```Constraint```, both the start and the end:

``` bash
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

**Try up your app now.**


## Interpolations
Duration: 0:10

A word about interpolations.

For each ```<Transition>``` we can define an interpolator.

* Go ahead and try on of the following : 

    <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/master/pics/Screen%20Shot%202018-11-29%20at%2010.39.39%20AM.png">
    
    
## Photos monipulations
Duration: 0:10

Images have a special set of attributes, we are going to explore some of them.

Let's go back to our image view settings : 

*   [Download](https://github.com/maozgal/MotionLayout/raw/image_manipulation/app/src/main/res/drawable/icon2.png) a new image and add it into your drawable folder.

*   We are using an ```ImageFilterView``` instead of a ```View``` in MainActivity.xml.

``` bash
 <android.support.constraint.utils.ImageFilterView
        android:id="@+id/main_iv"
        android:src="@drawable/icon2"
        android:layout_width="64dp"
        android:layout_height="64dp"/>
```
*   We created a new scene file : ```scene_03.xml```.
*   We changed the reference layoutDescription to point on ```@xml/scene_03``` : 

``` bash
app:layoutDescription="@xml/scene_03"
```
*   Copy the following into ```scene_03.xml```.

``` bash
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

You can also checkout [image_manipulation] (https://github.com/maozgal/MotionLayout/archive/image_manipulation.zip) branch.

* Saturation : 
    *   in ```scene_03.xml``` add a saturation CustomAttribute to the start and the end Constraint : 
    
     ``` bash
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
    
    **Try up your app now.**
    
* Contrast : 
    *   in ```scene_03.xml``` add a contrast CustomAttribute to the start Constraint : 
    
     ``` bash
    <CustomAttribute
                motion:attributeName="contrast"
                motion:customFloatValue="1" />
    ```
    
    and the end Constraint should get :
    
     ``` bash
    <CustomAttribute
                motion:attributeName="contrast"
                motion:customFloatValue="1" />
    ```
    
    **Try up your app now.**
    
* Warmth : 
    *   in ```scene_03.xml``` add a warmth CustomAttribute to the start Constraint : 
    
     ``` bash
    <CustomAttribute
                motion:attributeName="warmth"
                motion:customFloatValue="1" />
    ```
    
    and the end Constraint should get :
    
     ``` bash
    <CustomAttribute
                motion:attributeName="warmth"
                motion:customFloatValue="2" />
    ```
    
    **Try up your app now.**
    
* Altering an image with a fade : 
    *   in ```activity_main.xml```, Add altSrc to your ```ImageFilterView``` : 
    
    ``` bash
    <android.support.constraint.utils.ImageFilterView
        android:id="@+id/main_iv"
        android:src="@drawable/icon2"
        app:altSrc="@drawable/icon"
        android:layout_width="64dp"
        android:layout_height="64dp"/>
    ```
    
    *   in ```scene_03.xml``` add a crossfade CustomAttribute to the start and the end Constraint : 
    
     ``` bash
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
    
    **Try up your app now.**
    
## Swipes
Duration: 0:10

MotionLayout can handle the motion without any callbacks in your code. You can specify the dragging option in your XML scene.
The user will just swipe the views back and forth in order to animate them.
This swipe option isn't just to follow your finger. It also takes into account the acceleration and velocity.

Let's try it now.


*   Let's get rid of our buttons in ```activity_main.xml``` and delete handleViews() method from
```MainActivity.java```.

* : 

``` bash
app:layoutDescription="@xml/scene_04"
```

*   Copy the following into ```scene_04.xml```.

``` bash
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

*   Your ```activity_main.xml``` should look like : 

``` bash
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

``` bash
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
 **Try up your app now.**

## KeyFrame
Duration: 0:10

Until now, we defined a pair of start and end states and made animations between them.
You might ask your self, what if I want more than two states?

This is where KeyFrames are powerful.

The main idea of  KeyFrame is to give you tools to manipulate the animation in terms of size, color, rotation etc,  while it is been moving from the state 'start' to state 'end'.

On this slide, we will take an ```ImageView``` from bottom to top (centered horizontally), but this time we will add a KeyFrame that changes the bottom-up linear path into a diagonal path that goes from bottom-end to center-start and then to up-end.


*   Create a new scene file: ```scene_05.xml```.
*   Change the reference layoutDescription to point on ```@xml/scene_05``` : 

``` bash
app:layoutDescription="@xml/scene_05"
```

*   Copy the following into ```scene_05.xml```.

``` bash
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

*   Add the following below onSwipe

``` bash
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentX="0"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
</KeyFrameSet>
```

**Try up your app now.**

Explanation : 
*   ```percentX``` = Left of the parent.
*   ```framePosition``` = When on the timeline the action takes place.
*   ```target``` = The view on which the action will affect.


Let's try a more complicated ```KeyFrameSet```.

*   Replace your ```KeyFrameSet``` with the following :

``` bash
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

**Try up your app now.**

Other than we have ```KeyAttribute``` which allows you to play around with basic view attributes such as size, color, rotation etc.

Let's enlarge our view twice its size and rotate it -45 degrees at halfway of the animation:

*   Replace your ```KeyFrameSet``` with the following :

``` bash
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

**Try up your app now.**

And if we will go wild :

*   Replace your ```KeyFrameSet``` with the following :

``` bash
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

**Try up your app now.**

## Cool stuff with KeyFrames
Duration: 0:10

We can try some cool keyframe combinations.

*   Create a new scene file : ```scene_06.xml```.
*   Change the reference layoutDescription to point on ```@xml/scene_06``` : 

``` bash
app:layoutDescription="@xml/scene_06"
```

*   Copy the following into ```scene_06.xml```.

``` bash
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

* Go to ```activity_main.xml``` and add the following lines :

``` bash
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

Also, in ```activity_main.xml``` add : 

``` bash
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
    
And call handleViews() from onCreate()

*   Let's add the following lines itno ```<Transition>``` : 

``` bash
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

We can go wilder and do that : 


``` bash
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

**Try up your app now.**

## Arcs
Duration: 0:10

MotionLayout offers you the ability to transform a linear path between to points to an arch.

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/arcs/pics/arcs.png" width="500">

*   Create a new scene file : ```scene_07.xml```.
*   Change the reference layoutDescription to point on ```@xml/scene_07``` : 

``` bash
app:layoutDescription="@xml/scene_07"
```

*   Copy the following into ```scene_07.xml```.

``` bash
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

For this property, we want to actually see the path.
* Go to ```activity_main.xml``` and add the following line to the root view :

``` bash
app:showPaths="true"
```

* Go to ```scene_06.xml``` and add to the following line to the ```<Constraint>``` child of  ```<ConstraintSet android:id="@+id/start">``` : 

``` bash
motion:pathMotionArc="startHorizontal"
```

Like this :

``` bash
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


**Try up your app now.**

You can also decide that you want the arch to be only a part of the path and not all of it :

* Delete the following line from your end ```<Constraint>```: 

``` bash
motion:layout_constraintStart_toStartOf="parent"
```

* Add the following lines to your ```<Transition>``` : 


``` bash
<KeyFrameSet>
    <KeyPosition
        motion:keyPositionType="parentRelative"
        motion:percentY="0.5"
        motion:pathMotionArc="none"
        motion:framePosition="50"
        motion:target="@id/main_iv"/>
</KeyFrameSet>
```

**Try up your app now.**

* Chane pathMotionArc to : 

``` bash
motion:pathMotionArc="flip"
```

**Try up your app now.**

## Monitor
Duration: 0:10

The last feature we will present is a tool that lets you monitor your animation manually.
We will pass the control of the animation to a ```Seekbar```. This way you can understand exactly what is happening in every frame of your scene.

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/monitor/pics/vid.gif" width="250">

We can control the progress of a ```MotionLayout``` by setProgress() method.

*   Let's get rid of our buttons in ```activity_main.xml```, and add a seekbar instead : 

``` bash
<android.support.v7.widget.AppCompatSeekBar
        android:id="@+id/seek"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        android:layout_marginBottom="10dp"/>
```


*   On ```MainActivity.java```, change handleViews() method to : 

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

**Try up your app now.**
