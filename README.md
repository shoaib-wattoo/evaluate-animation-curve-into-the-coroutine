## Objective
Main Objective of this blog post is to give you an idea about Evaluate AnimationCurve into the Co-routine.


## Step 1 : What is AnimationCurve

Generally we use AnimationCurve into the Animation clip. Any animation property can have an AnimationCurve, which means that the Animation Clip controls that property.

**AnimationCurve** has multiple keys which are the control points through which the curve passes. These are visualized in the Curve Editor as small diamond shapes on the curves. A frame, in which one or more of the shown curves have key, is called the keyframe.

If a property has key in the currently previewed frame, the curve indicator will have a diamond shape.

**AnimationCurve:** “Create an **animation curve** from the arbitrary number of key frames. This creates a curve from variable number of key frame parameters. If you want to create a curve from an array of key frames, create an empty curve and assign keys properties.”

## Step 2 : Why we need it?

**Why do we need to use AnimationCurve into the Co-routine?**

Sometimes, we make UI animations by making Co-routines, which has some arguments (i.e. startPosition, endPosition or startRotation, endRotation). By using these arguments we are moving object smoothly from starting position to the end position or rotating object smoothly from starting rotation to ending rotation.

This can also be achieved by using an Animation clip. But here starting and ending position to move the Game Object may vary, and same for the rotation. At that time we can use Co-routine to perform an animation by passing dynamic values.

## Step 3 : Implementation

AnimationCurve has one method:

```csharp
public float Evaluate(float time);
```
Declare AnimationCurve in any Game Object Script that you want to animate:

```csharp
public AnimationCurve animationCurve;
```

**Starting and Ending Position:**

public Vector3 startPosition;
public Vector3 endPosition;
public float animationTime; 

![](http://www.theappguruz.com/app/uploads/2015/06/animation-curve.png)

=> Set curve as per your requirement by clicking on that: 

![](http://www.theappguruz.com/app/uploads/2015/06/curve-as-per-your-requirement.png)

=> Make your own AnimationCurve by adding keys.

```csharp
private bool isAnimationRunning=false;
```
Co-routine Where I have evaluated the AnimationCurve:

```csharp
IEnumerator UsingAnimationCurve(Vector3 startPosition, Vector3 endPosition, float time)   {
if (!isAnimationRunning){
isAnimationRunning = true;
float i = 0.0f;
float rate = 1 / time;
while (i < 1)
{
i += Time.deltaTime * rate;
transform.localPosition=Vector3.Lerp(startPosition,endPosition, animationCurve.Evaluate(i));
yield return 0;
}
isAnimationRunning = false;
}
yield return 0;
}
```

**Now, Start the Co-routine:**

```csharp
StartCoroutine(UsingAnimationCurve(startPosition, endPosition, animationTime));
```

**AnimationCurve use:**

```csharp
“transform.localPosition=Vector3.Lerp(startPosition,endPosition, animationCurve.Evaluate(i));”
```

Here, the value of **i** will handle your animation curve.

It will calculate and return new value into the Vector3.Lerp() method.

And According to that value new position will be set.

**By, using AnimationCurve you can give a variety of animation effectss just by using the same method.**
