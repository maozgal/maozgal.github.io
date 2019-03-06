author: Gal Maoz
summary: Flexbox Workshop
id: galm_flexbox_layout
categories: LAyouts
environments: Android



# Android FlexboxLayout 101

## Introduction
Duration: 1:00


This Codelab will walk you through everything you need to know about FlexboxLayout in Android.

You'll learn the following concepts:

* Handling Flexbox's directions, alignments and sizes as a ViewGroup.

* Handling individual item's kinds of behaviors.

* Using Flexbox as LayoutManager for RecyclerView.

Hope you'll enjoy the Codelab!.


The source code for this codelab can be found on [Github](https://github.com/maozgal/FlexboxLayoutWorkshop).

## Setup Your Environment
Duration: 3:00

In this step, you will download the code for the entire Codelab and run a simple example app.

Click the following link to download the source code for this codelab:
  [Download Code Lab sources](https://github.com/maozgal/FlexboxLayoutWorkshop/archive/master.zip)

*   Unzip the code, and open the project.
*   Run the app <img src="https://raw.githubusercontent.com/maozgal/MotionLayout/solution/pics/Screen%20Shot%202018-11-27%20at%203.34.27%20PM.png" width="100">

You should see a blank app that looks like this:

<img src="device-2019-01-17-180551.png" width="250">

Feel free to visit us on GitHub.

## First Steps
Duration: 8:00


Go to res -> ```activity_main.xml```, and add the following line inside your ```ConstraintLayout``` root view :

``` xml
<com.google.android.flexbox.FlexboxLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">

</com.google.android.flexbox.FlexboxLayout>
```

Here you just adding the ```FlexboxLayout``` element.

The ```FlexboxLayout``` is the element in charge of arranging our items, so next thing is to add some elements.

Add 3 ```ImageView```s with a nice dog image as direct sons of the ```FlexboxLayout```.

``` xml
<com.google.android.flexbox.FlexboxLayout
      android:layout_width="match_parent"
      android:layout_height="match_parent">

      <ImageView
          android:layout_width="60dp"
          android:layout_height="60dp"
          android:src="@drawable/dog"/>

      <ImageView
          android:layout_width="60dp"
          android:layout_height="60dp"
          android:src="@drawable/dog"/>

      <ImageView
          android:layout_width="60dp"
          android:layout_height="60dp"
          android:src="@drawable/dog"/>
  </com.google.android.flexbox.FlexboxLayout>
```

**Run the app.**
It should look like this:
<img src="device-2019-02-04-180855.png" width="250">


## FlexDirection
Duration: 5:00

Using ```FlexboxLayout``` you can determine the direction from which your items will be arranged, you can choose to arrange them one by one as rows, as columns or, to reverse their insertion order.

The attributes are as following:
*   row.
*   row_reverse
*   column
*   column_reverse



In your ```activity_main.xml``` add the following line to your ```FlexboxLayout```:

``` xml
app:flexDirection="column"
```
It should look like this:
<img src="device-2019-02-04-180632.png" width="250">

Now, chage it to :

``` xml
app:flexDirection="column_reverse"
```
It should look like this:
<img src="device-2019-02-04-181648.png" width="250">

Chage it to :

``` xml
app:flexDirection="row"
```
It should look like this:
<img src="device-2019-02-04-180855.png" width="250">

Last, change it to :

``` xml
app:flexDirection="row_reverse"
```
It should look like this:
<img src="device-2019-02-04-181359.png" width="250">


To summarize, ```flexDirection``` attribute tells ```FlexboxLayout``` from where to start arrange items.

Cool, hha?

Now that you know how to decide your ```flexDirection```, we can move on to next chapter.
For that, your ```FlexboxLayout``` should look like this :
``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row">

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```


## FlexWrap
Duration: 4:00

After you've decided what is your ```flexDirection```, it is time to choose if your layout will be a single-line or a multi-line layout.

The attributes are as following:
*   nowrap (single-line)
*   wrap (nulti-line)
*   wrap_reverse

Add 7 more ```ImageView```s so that your ```FlexboxLayout``` will contain 10 items.

Now add the following line to your ```FlexboxLayout```:

``` xml
app:flexWrap="wrap"
```

Your layout should look like this:
``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="wrap">

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```
And the outcome of it is like this:
<img src="device-2019-02-05-091433.png" width="250">

Change your ```flexWrap``` to :

``` xml
app:flexWrap="nowrap"
```

The outcome of this should like:
<img src="device-2019-02-05-091742.png" width="250">

Change your ```flexWrap``` it to :

``` xml
app:flexWrap="wrap_reverse"
```

The outcome of this should like:
<img src="device-2019-02-05-091910.png" width="250">

For the next step, delete tow of your nice little doggies ImageViews, and change the flexwrap to wrap

The layout should look like this:

``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="wrap">

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```
## JustifyContent

Duration: 5:00

Up until now we can manipulate the way in which ```FlexboxLayout``` will arrange the items regarding their starting point, direction ect.
But what if we want to control the space between the items themselves??

The ```justifyContent``` is your answer! it is the attribute in charge of how your items will be aligned to each other.
The possibilities are as follow:

* flex_start (start arrange from the start without spacing between the items)
* flex_end  (start arrange from the end without spacing between the items)
* center (arrange the items to be center without spacing)
* space_between (arrange the items to have space between themselves as much as possible)
* space_around (arrange the items to have space between themselves and also have space from the edges of the layout)

Start by adding the following line to your ```FlexboxLayout```:

``` xml
app:justifyContent="center"
```

That should look like this:
<img src="device-2019-02-06-135248.png" width="250">

Change it to :

``` xml
app:justifyContent="space_between"
```

That should look like this:
<img src="device-2019-02-06-141528.png" width="250">

Change it to :

``` xml
app:justifyContent="space_around"
```

That should look like this:
<img src="device-2019-02-06-142350.png" width="250">

Change it to :

``` xml
app:justifyContent="flex_start"
```

That should look like this:
<img src="device-2019-02-06-142625.png" width="250">

flex_end is just the opposite of flex_start.

Great!
You should note an important thing here.
Every layout has X and Y axises. X is the horizontal while Y is the vertical.
In ```FlexboxLayout``` you don't use the terms horizontal or vertical. instead you have a main axis and a cross axis.
Those are flexible to your needs, you decide if the main axis will be horizontal or vertical by ```flexDirection``` you have already met.

By using ```justifyContent```, you determine the behavior of main axis(a.k.a flex line).
The treatment of the cross axis's behavior will be in the next step ```alignItems```.

Well, now you know ```justifyContent``` :)

Positive
: Note : In ```FlexboxLayout``` you don't use the terms horizontal or vertical. instead you have a main axis and a cross axis.


Here is the code for the next step:

``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="wrap"
        app:justifyContent="space_between">

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```

## AlignItems
Duration: 4:00

As mentioned in the paragraph above, ```alignItems``` is about control the arrangement of your cross axis.

These are your possibilities:

* stretch
* flex_start
* flex_end
* center
* baseline

Bare in mind that we are demonstration only part of the permutations that ```FlexboxLayout``` has to offer since we already used :
``` xml
app:flexDirection="row"
app:flexWrap="wrap"
app:justifyContent="space_between"
```
Also, We will not explore all the possibilities of ```alignItems``` since some of them looks the same under the above parameters.
Start by adding the following line to your ```FlexboxLayout```:

``` xml
app:alignItems="flex_start"
```

That should look like this:
<img src="device-2019-02-11-183822.png" width="250">


Change it to :

``` xml
app:alignItems="flex_end"
```

That should look like this:
<img src="device-2019-02-11-184307.png" width="250">


Change it to :

``` xml
app:alignItems="center"
```

That should look like this:
<img src="device-2019-02-11-184703.png" width="250">

``` xml
<com.google.android.flexbox.FlexboxLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       app:flexDirection="row"
       app:flexWrap="wrap"
       app:justifyContent="space_between"
       app:alignItems="center">

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

   </com.google.android.flexbox.FlexboxLayout>
```


## AlignContent
Duration: 4:00

In order to control the spac between the lines of the cross axis, you will want to use ```alignContent```

You can use the following attributes for that:

* stretch
* flex_start
* flex_end
* center
* space_between
* space_around

Lets explore some of them.
Start by adding the following line to your ```FlexboxLayout```:

``` xml
app:alignContent="flex_start"
```

That should look like this:
<img src="device-2019-02-12-184444.png" width="250">

Change it to :

``` xml
app:alignItems="space_between"
```

That should look like this:
<img src="device-2019-02-12-184609.png" width="250">

Change it to :

``` xml
app:alignItems="flex_end"
```

That should look like this:
<img src="device-2019-02-12-184810.png" width="250">


Here is the code for the next step:

``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="wrap"
        app:justifyContent="space_between"
        app:alignItems="center"
        app:alignContent="flex_end"
        >

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```

## Dividers
Duration: 4:00

With ```FlexboxLayout``` You can add dividers in between your items. You have horizontal and vertical dividers.
For Each direction you can specify a different drawable and a set of attributes.

Let's get our hands dirty :)

You will use two drawables as dividers.

Go to res -> drawable ,and create two new resource XML files under the names : ```vertical_divider.xml``` and ```horizontal_divider.xml```.

Copy the following to ```vertical_divider.xml``` :

``` xml
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <size
        android:width="8dp"
        android:height="12dp" />
    <solid android:color="#00FF21" />
</shape>
```

Copy the following to ```horizontal_divider.xml``` :

``` xml
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <size
        android:width="8dp"
        android:height="12dp" />
    <solid android:color="#FF0000" />
</shape>
```

Add an horizontal divider by doing the following :
Go to res -> ```activity_main.xml```, and add the following line inside your ```FlexboxLayout```:

``` xml
app:dividerDrawableHorizontal="@drawable/horizontal_divider"
```

Next, you need to specify how do you want the dividers to appear.
You will do that by a combination of one or more of the attributes :

* none
* beginning
* middle
* end

Add the following line inside your ```FlexboxLayout```:

``` xml
app:showDividerHorizontal="middle|beginning"
```

That should look like this:
<img src="device-2019-02-14-190005.png" width="250">

Try play alonog with the parameters.


Add the following lines inside your ```FlexboxLayout``` in order to set a vertical divider.:

``` xml
app:dividerDrawableVertical="@drawable/divider_vertical"
app:showDividerVertical="middle"
```

That should look like this:
<img src="device-2019-02-17-161840.png" width="250">

You can also set one divider and one behavior for both vertical and horizontal dividers.

Up until now we tried all kinds of setups ```FlexboxLayout``` has to offer as a layout.
The next steps will cover the set of behaviors ```FlexboxLayout``` offers to its children.

## Layout Order
Duration: 4:00

The chapters from now on will be focused on the abilities that ```FlexboxLayout``` grant it children.

Go to res -> ```activity_main.xml```, and add the following inside your ```ConstraintLayout``` root view :

``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="wrap"
        app:justifyContent="flex_start"
        app:alignItems="center"
        app:alignContent="flex_start">

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/cat"/>

    </com.google.android.flexbox.FlexboxLayout>
```

Your app should look like this now :
<img src="device-2019-02-19-183621.png" width="250">

Pay attention we have now a cute little cat as our last child.

Say you to control the order of your items...
For example - to make the cat be first child, before all the dogs.

For that porpse, you will use ```layout_order``` attribute.

In your layout, go to the last child (the one with the cat drawable), and add the following line:

``` xml
app:layout_order="1"
```

Nothing happened?? that is because 1 is the default value for items that without ```layout_order``` set.

Change the line to:
``` xml
app:layout_order="0"
```

Your app should look like this now :
<img src="device-2019-02-20-085209.png" width="250">


For the next chapter you will need to set your layout as following:
``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="wrap"
        app:justifyContent="flex_start"
        app:alignItems="center"
        app:alignContent="flex_start"
        app:dividerDrawable="@drawable/divider_vertical"
        app:showDivider="middle|beginning|end">

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/cat"/>

    </com.google.android.flexbox.FlexboxLayout>
```

##Layout FlexGrow
Duration: 4:00

As ```FlexboxLayout``` arrange the item one by one, sometimes you there will be a gap between the last item and the rest of the layout or between items.
This gap can be filled by spreading an item along it.

You will use ```layout_flexGrow``` attribute for that. ```FlexboxLayout``` will calculate the gap on each flex line, and divide it between the items that specified  the ```layout_flexGrow``` proportionally to their value (For those who familiar with ```LinearLayout```,  the behavior is similar to ```layout_weight``` attribute).


In your layout, go to the last child (the one with the cat drawable), and add the following line:

``` xml
app:layout_flexGrow="2.0"
```

So the item will look like:

``` xml
<ImageView
  app:layout_flexGrow="2.0"
  android:background="#FF00"
  android:layout_width="60dp"
  android:layout_height="60dp"
  android:src="@drawable/cat"/>

```

Your app should look like this now :
<img src="device-2019-02-20-091302.png" width="250">


In your layout, go to the one before the cat item, and add the following line:

``` xml
app:layout_flexGrow="7.0"
```

Your app should look like this now :
<img src="device-2019-02-20-181806.png" width="250">



##Layout FlexShrink
Duration: 4:00

In ```flexWrap``` chapter, you learned that when ```FlexboxLayout```  specifies that ``` app:flexWrap="nowrap" ```, the layout will be single line. That means that whenever you will add a new item, if there is not enough space - ```FlexboxLayout``` will make the items shrink so that they all will fit inside.

By using ```layout_flexShrink``` we can control this operation and define which items will get shrink and how much.
Bare in mind that the default value here is 1, so each undefined item will get value of 1.

Go to res -> ```activity_main.xml```, and add the following inside your ```ConstraintLayout``` root view :

``` xml
<com.google.android.flexbox.FlexboxLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       app:flexDirection="row"
       app:flexWrap="nowrap"
       app:justifyContent="flex_start"
       app:alignItems="center"
       app:alignContent="flex_start"
     >

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/cat"/>

   </com.google.android.flexbox.FlexboxLayout>
```

Your app should look like this now :
<img src="device-2019-02-21-182208.png" width="250">

If for example the cat is not so important, you can say that when there is not enough space, the cat will get shrink by 5 times more than the other items (since thier value is 1 and we are setting the cat's to 5) of the other items by adding the following line to its ```ImageView```:

``` xml
app:layout_flexShrink="5"
```

The ```ImageView``` should be define like this:

``` xml
<ImageView
  app:layout_flexShrink="5"
  android:background="#FF00"
  android:layout_width="60dp"
  android:layout_height="60dp"
  android:src="@drawable/cat"/>
```


Your app should look like this now :
<img src="device-2019-02-21-183551.png" width="250">

##Layout AlignSelf
Duration: 4:00

In the chap above we mentioned that the differences between ```justifyContent``` and ```alignItems``` is that the first controls the behavior of the main axis, while the second handles the cross axis.

These attributes handles the direction of order on parent lavel.
Sometimes you will want to have a more specific direction handling, ```layout_alignSelf``` will help you achieve that on a child level.

For the current demonstration, take the following layout:

``` xml
<com.google.android.flexbox.FlexboxLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       app:flexDirection="row"
       app:flexWrap="wrap"
       app:justifyContent="flex_start"
       app:alignItems="flex_start"
       app:alignContent="flex_start">

       <ImageView
           android:background="#FF00"
           android:layout_width="160dp"
           android:layout_height="160dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FF00"
           android:layout_width="60dp"
           android:layout_height="60dp"
           android:src="@drawable/cat"/>

   </com.google.android.flexbox.FlexboxLayout>
```

It should look like the following:
<img src="device-2019-02-24-163102.png" width="250">

Add the following line to the second child:

``` xml
app:layout_alignSelf="flex_end"
```

The item shloud look like this:

``` xml
<ImageView
    app:layout_alignSelf="flex_end"
    android:background="#FF00"
    android:layout_width="60dp"
    android:layout_height="60dp"
    android:src="@drawable/dog"/>
```

And your app should look like this:
<img src="device-2019-02-24-163605.png" width="250">

You can play around with the parameters:
* auto
* flex_start
* flex_end
* center
* baseline
* stretch


##Layout FlexBasisPercent
Duration: 4:00

In case that you want to determine the length of an item based on its parent, ```layout_flexBasisPercent``` will solve your problem here.
The length here refers to the main axis.

Note : It will not work for parent with ```layout_width="wrap_content"```.

For the current demonstration, take the following layout:

``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="wrap"
        app:justifyContent="flex_start"
        app:alignItems="flex_start"
        app:alignContent="flex_start">

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FF00"
            android:layout_width="60dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```

It should look like the following:
<img src="device-2019-02-25-185217.png" width="250">

Add the following line to the second child:

``` xml
app:layout_flexBasisPercent="50%"
```

Be aware to the ```%```. Yes oddly you need to add that sign to the value.

So, your second child should look like this:

``` xml
<ImageView
  app:layout_flexBasisPercent="50%"
  android:background="#FF00"
  android:layout_width="60dp"
  android:layout_height="60dp"
  android:src="@drawable/dog"/>
```

And your app should look now like the following:
<img src="device-2019-02-25-185711.png" width="250">


The second now has a width of 50% of its parent.


##Layout MinWidth / MinHeight
Duration: 4:00

Since ```FlexboxLayout``` will shrink items when needed, you might want to set some constraint on the shrinking behavior.
You can set a minimum width from which the view cannot get shrink.

For the current demonstration, take the following layout:

``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="nowrap"
        app:justifyContent="flex_start"
        app:alignItems="flex_start"
        app:alignContent="flex_start">

        <ImageView
            android:background="#FF00"
            android:layout_width="160dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#00F"
            android:layout_width="160dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```

It should look like the following:
<img src="device-2019-02-26-182611.png" width="250">

Now, add the following two ```ImageView```s, pay attention to how ```FlexboxLayout``` will shrink the width of all of your ```ImageView```s equally.

``` xml
<ImageView
    android:background="#FFF0"
    android:layout_width="160dp"
    android:layout_height="60dp"
    android:src="@drawable/dog"/>

<ImageView
    android:background="#F0F0"
    android:layout_width="160dp"
    android:layout_height="60dp"
    android:src="@drawable/dog"/>
```

So, your ```FlexboxLayout``` should look like this:

``` xml
<com.google.android.flexbox.FlexboxLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:flexDirection="row"
        app:flexWrap="nowrap"
        app:justifyContent="flex_start"
        app:alignItems="flex_start"
        app:alignContent="flex_start">

        <ImageView
            android:background="#FF00"
            android:layout_width="160dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#00F"
            android:layout_width="160dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#FFF0"
            android:layout_width="160dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

        <ImageView
            android:background="#F0F0"
            android:layout_width="160dp"
            android:layout_height="60dp"
            android:src="@drawable/dog"/>

    </com.google.android.flexbox.FlexboxLayout>
```

And your app should look now like the following:
<img src="device-2019-02-26-183041.png" width="250">


Go to your second ```ImageView``` (the one with the blue background), and add the following line:

``` xml
app:layout_minWidth="150dp"
```

Your app should look now like the following:
<img src="device-2019-02-26-183524.png" width="250">

This way you can keep the minimum width constraint.
Similarly you can use the ```layout_minHeight```.

With that in mind, handling the maximum is almost the same. Just use ```layout_maxWidth``` / ```layout_maxHeight```.

##Layout WrapBefore
Duration: 4:00

As ```FlexboxLayout``` behaves like a grid, if you want to start a new flex line from a specific item, you'll do that by using ```layout_wrapBefore```.

For the current demonstration, take the following layout:

``` xml
<com.google.android.flexbox.FlexboxLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       app:flexDirection="row"
       app:flexWrap="wrap"
       app:justifyContent="flex_start"
       app:alignItems="flex_start"
       app:alignContent="flex_start">

       <ImageView
           android:background="#FF00"
           android:layout_width="100dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#00F"
           android:layout_width="100dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#FFF0"
           android:layout_width="100dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

       <ImageView
           android:background="#F0F0"
           android:layout_width="100dp"
           android:layout_height="60dp"
           android:src="@drawable/dog"/>

   </com.google.android.flexbox.FlexboxLayout>
```

It should look like the following:
<img src="device-2019-02-27-175304.png" width="250">

Go to your second ```ImageView``` (the one with the blue background), and add the following line:

``` xml
app:layout_wrapBefore="true"
```

Your app should look now like the following:
<img src="device-2019-02-27-175435.png" width="250">

As you can see, this attribute 'broke' the line.

Note: It will not work for layouts which specified ```app:flexWrap="nowrap"```, since it is single line and there is now meaning for 'breaking a line' there.

##FlexboxLayout as LayoutManager.
Duration: 4:00

The last chapter will describe the steps of using ```FlexboxLayout``` as ```LayoutManager```.
The advangtage here is that you have a scrollable View that can host an infinite number of them with the abilities of ```Flexbox```.

You will start by changing the layout to the following:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    tools:context=".MainActivity">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler_view"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toTopOf="@id/add_item_button"/>

    <Button
        android:id="@+id/add_item_button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Add an Item"
        app:layout_constraintBottom_toBottomOf="parent"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```
We have a ```Recyclerview``` and a ```Button```.

Next thing you need is to define how a single item will look like.

Go to res -> drawable ,and create new resource XML file under the name : ```item_background.xml```.

Copy the following into ```item_background.xml```:

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <stroke android:width="2dp" android:color="#ac5c23" />
    <corners android:radius="12dp"/>
    <solid android:color="#ffbb00" />
</shape>
```

Go to res -> layout ,and create new resource XML file under the name : ```item.xml```.

Copy the following into ```item.xml```:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        android:background="@drawable/item_background"
        android:padding="15dp"
        android:layout_margin="5dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```

Last setup step is to create a simple Adapter for the ```Recyclerview```:

Create a new class called ```SimpleAdapter``` and fill it with the following:  

``` kotlin
class SimpleAdapter(private val mItems: ArrayList<String>) : RecyclerView.Adapter<SimpleAdapter.DivItemViewHolder>() {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): SimpleAdapter.DivItemViewHolder {
        val view = LayoutInflater.from(parent.context)
                .inflate(R.layout.item, parent, false)
        return DivItemViewHolder(view)
    }

    override fun onBindViewHolder(holder: DivItemViewHolder, position: Int) {
        holder.onBind(position)
    }

    override fun getItemCount(): Int {
        return mItems.size
    }

    inner class DivItemViewHolder constructor(itemView: View) : RecyclerView.ViewHolder
    (itemView) {
        private val text: TextView = itemView.findViewById(R.id.text)

        fun onBind(position: Int) {
            text.text = mItems[position]
        }
    }
}
```

You will now build you ```LayoutManager```.

Go the ```MainActivity```, and add the following to your ```onCreate``` method:

``` kotlin
val layoutManager = FlexboxLayoutManager(this)
layoutManager.flexDirection = FlexDirection.ROW
layoutManager.justifyContent = JustifyContent.CENTER
```

This is simply creates a ```FlexboxLayoutManager``` the it's main axis is ROW and these rows are arranging their item in a flexbox CENTER manner.

Keep up with the following code to set the ```LayoutManager``` to your ```RecyclerView```:

``` kotlin
recycler_view.layoutManager = layoutManager
```

Now, build a list with some content you can insert into the ```Adapter```:

``` kotlin
val divLikeContent = ArrayList<String>()
divLikeContent.add("Route")
divLikeContent.add("No calls during the ride")
divLikeContent.add("Smell")
divLikeContent.add("Less talk")
divLikeContent.add("Safety")
```

Create a ```SimpleAdapter``` and set the ```RecyclerView``` with it:

``` kotlin
val adapter = SimpleAdapter(contentList)

recycler_view.adapter = adapter
```
You'll create a logic for adding an item with random amount of letters in order to illustrate how ```FlexboxLayoutManager``` arranging the items by thier size.

Set a ```ClickListener``` to the Button:

``` kotlin
add_item_button.setOnClickListener {
    contentList.add(generateRandonText())
    recycler_view.adapter = adapter
}
```

Add the ```generateRandonText()``` method in the class scope.

``` kotlin
private fun generateRandonText(): String {
    val sb = StringBuilder()
    for (i in 1 + (Math.random() * 20).toInt() downTo 1) {
        sb.append("a")
    }
    return sb.toString()
}
```

Run your app and click the button.
Also, try play around with the parameters to achieve the behaviors you just learn so far.

Here is an example with some random items:

<img src="device-2019-03-05-184053.png" width="250">



Well, our journey ends here, thanks you for flying with us :)

For further questions, you are more than welcome to find me at [@maozgal](https://twitter.com/maozgal) 
