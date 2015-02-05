Prajwal Manjunath

D2: Collision Detection Mathematics

Data structures assumed:
* Vector2(x, y)
* 


Rectangle-Rectangle collision:
------------------------------

Signature: Rect(Vector2 min, Vector2 max)

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

Circle-Circle collision:
------------------------

Signature: Circle(Vector2 centre, float radius)

```
function IsColliding(Circle c1, Circle c2) {
    float dist = Vector2.length(c2.center - c1.center);
    return (dist < c1.radius + c2.radius);
}
```


