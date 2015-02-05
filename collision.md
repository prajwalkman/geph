**Prajwal Manjunath** | _pmanjuna@andrew.cmu.edu_ | 2/5/2015

***D2: Collision Detection Mathematics***

Data structure:
* Vector2(x, y)
* Vector2.Dot(Vector2 other) => x * other.x + y * other.y
* Vector2.Length => Math.Sqrt(Dot(this))
* Vector2.Perpendicular => Vector2(-y, x)


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
    return Vector2.length(c2.center - c1.center) < c1.radius + c2.radius;
}
```

Convex-Convex collision:
------------------------

Signature: Poly(Vector2[] vertices)

Method: Separating Axis Theorem

```
function IsColliding(Poly p1, Poly p2) {
    
    // subroutine to project a polygon onto an axis
    Vector2 Projection => (Vector2 axis, Poly p) {
        float min = infinity;
        float max = -infinity;
        foreach (v in p.vertices) {
            float cur = axis.Dot(v);
            if (cur < min) min = cur;
            if (cur > max) max = cur;
        }
        return Vector2(min, max);
    }
    
    // subroutine to check if 2 projections overlap
    bool Overlap => (Vector2 a1, Vector2 a2) {
        return (a2.x > a1.x && a2.x < a1.y)
            || (a2.y > a1.x && a2.y < a1.y);
    }
    
    Vector2[] axesToTest;
    foreach (v in p1, p2)
        axesToTest.push((v - (v + 1)).Perpendicular);
    foreach (a in axesToTest) {
        proj1 = Projection(a, p1);
        proj2 = Projection(a, p2);
        if (!Overlap(proj1, proj2)) return false;
    }
    return true;
}

```
