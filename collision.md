Prajwal Manjunath

D2: Collision Detection Mathematics

Data structures assumed:
* Vector2(x, y)
* Vector2.Dot(Vector2 other) => x * other.x + y * other.y
* Vector2.Length => Math.Sqrt(Dot(this))


Rectangle-Rectangle collision:
------------------------------

Signature: Rect(Vector2 min, Vector2 max)

Method: Check if bounds overlap on both axes

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

Method: Check if distance between the centres is less than the sum of the radii

```
function IsColliding(Circle c1, Circle c2) {
    float dist = Vector2.length(c2.center - c1.center);
    return (dist < c1.radius + c2.radius);
}
```

Convex-Convex collision:
------------------------

Signature: Poly(Vector2[] vertices)

Method: Separating Axis Theorem

```


```
