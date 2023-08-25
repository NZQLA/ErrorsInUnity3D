# DG.Tweening.TweenExtensions.WaitForCompletion

## ErrorInfo:
```c#
NullReferenceException: Object reference not set to an instance of an object
DG.Tweening.TweenExtensions.WaitForCompletion (DG.Tweening.Tween t) (at D:/DG/_Develop/__UNITY3_CLASSES/_Holoville/__DOTween/_DOTween.Assembly/DOTween/TweenExtensions.cs:341)
```

## Example 1
```C#
// here is one gameObject
GameObject obj;
// if it's eulerAngle is (0, 0, 0)
obj.eulerAngles = new Vector3(0, 0, 0);

// but if you also want to rotate it to (0, 0, 0)
float start = 0;
float end = 0;
float current = start;

// use the following code
var tween = DOTween.To(() => current, (v) =>
    {
        current = v;
        self.rotation = originRota;
        self.Rotate(axis, v, space);
    }, angleTotal, duration);

// and then use the following code in one IEnumerator function
yield return tween.WaitForCompletion();
// you will get the error
// NullReferenceException: Object reference not set to an instance of an object
// DG.Tweening.TweenExtensions.WaitForCompletion (DG.Tweening.Tween t) (at D:/DG/_Develop/__UNITY3_CLASSES/_Holoville/__DOTween/_DOTween.Assembly/DOTween/TweenExtensions.cs:341)
```
- WaitForCompletion SourceCode:
```C#
public static YieldInstruction WaitForCompletion(this Tween t)
{
    //=================================
    if (!t.active)
    {
        if (Debugger.logPriority > 0)
        {
            Debugger.LogInvalidTween(t);
        }

        return null;
    }
    //=================================


    return DOTween.instance.StartCoroutine(DOTween.instance.WaitForCompletion(t));
}
```

## Reason:<br/>
The tween is not active or null, beause it need't do it, it's current data is equal to the target data! <br/>


## Solution:<br/>
Ensure the tween is active before you call WaitForCompletion()<br/>
<span style="color:#00ff00">Avoid  let the tween's from = to</span><br/>



