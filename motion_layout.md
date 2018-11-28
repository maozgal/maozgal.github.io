author: Gal Maoz
summary: Some MotionLayout Crafts
id: galm_motion_layout
categories: Animations
environments: Android



# Some MotionLayout Crafts

## Introduction
Duration: 0:05


This tutorial will walk you through the way of creating your first  MotionLayout steps. In this tutorial you will do the following, using MotionLayout:

* Basic animation.
* Apply the newly created style
Prerequesites
* API key
* Npm and Node.js
We recommend you to have npm and Node.js already installed on your machine to quickly boot up a http server.


Positive
: Note : MotionLayout is fully declarative. therefore, we will not use any code for animate



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
The whole solution can be found on [solution](https://github.com/maozgal/MotionLayout/tree/solution) branch.

 

## Basic Animation
Duration: 0:10

First thing we want to do is to denote the layout that we want to take control of several of it's view.

This is being done by adding layoutDescription parameter to the root view, which just points to the file where the animations are being described.

* Go to res -> ```activity_main.xml```, and add the following line into your MotionLayout root view : 



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

Next step is to create the scene_01 file.
* Create ```xml``` folder under res.
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

Explaination:
In order to take control of an animation, we need to define a ```MotionScene```.
MotionScene is describing the animation. in our case we will make a tranistion from point A to point B on the screen, with a duration of 1 second.
 
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


Explaination:
Take a look at the ```<Constraint>``` of ```@+id/start``` ConstraintSet,
* We define the view on which we will want the animation to affect(```@+id/main_iv```).
* Next, we will define it's constraints. These constraints will be affect imidiitlly, as a start stage. The current constaints are centering the view vertically and attach it to the left.

The constaints in ```@+id/end``` are the same. only difference is attaching the view to the right.

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

Try and run your app now.
You should be able to animate the view back and forth by clicking the buttons.



## Attributes
Duration: 0:10

Click the following button to download the source code for this codelab:
  [Download SDK](https://github.com/maozgal/MotionLayout/archive/attributes.zip)

*   Unzip the code, and then open the project.
*   Run the app <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%203.34.27%20PM.png" width="100">

The app you should be looking like this:

<img src="https://raw.githubusercontent.com/maozgal/MotionLayout/attributes_solution/pics/device-2018-11-28-184148.png" width="250">


Pay attention to the following changes.

1.  We are using a View instade of an ImageView in MainActivity.xml.

``` bash
 <View
        android:id="@+id/main_iv"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:background="@color/colorAccent"
        />
```
2.  We created a new scene file : scene_02.xml.
3.  We changed the refernce layoutDescription to point on @xml/scene_02 : 

``` bash
app:layoutDescription="@xml/scene_02"
```
4.  In scene_02.xml we constrainted our view to center horizontal + bottom at start, and center horizontal + top at the end of the animation.

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

Try up your app now.

*   Alpha :
    *   Add the following ```CustomAttribute``` into your start ```Constraint```

        ``` bash
        android:alpha="1.0"
        ```
    
    *   Add the following ```CustomAttribute``` into your end ```Constraint```

        ``` bash
        android:alpha="0.5"
        ```
Try up your app now.

*   Rotation :
    *   Add the following ```CustomAttribute``` into your start ```Constraint```

        ``` bash
        android:rotation="0.0"
        ```
    
    *   Add the following ```CustomAttribute``` into your end ```Constraint```

        ``` bash
        android:rotation="-720"
        ```
Try up your app now.

*   Translation :
    *   Add the following ```CustomAttribute``` into your start ```Constraint```

        ``` bash
        android:translationX="0dp"
        ```
    
    *   Add the following ```CustomAttribute``` into your end ```Constraint```

        ``` bash
        android:translationX="100dp"
        ```
Try up your app now.

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
