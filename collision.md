Prajwal Manjunath

D2: Collision Detection Mathematics

Data structures assumed:
* Vector2(x, y)
* 


Rectangle-Rectangle collision:
------------------------------

Signature: Rect(Vector2 min, Vector2 max)

Pseudocode:
```
function IsColliding(Rect r1, Rect r2) {
    if (r1.min.x < r2.max.x)
        if (r1.max.x > r2.min.x)
            if (r1.min.y < r2.max.y)
                if (r1.max.y > r2.min.y)
                    return true;
    return false;
}
```

