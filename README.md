# Spirograph Vizualization

A JS implementation of a [Spirograph](https://en.wikipedia.org/wiki/Spirograph). Basically vizualizations of geometrical figures that are visually appealing.

## Mathematical Working

I haven't checked all the math yet, please feel free to correct me if something
looks wrong.

Let's imagine we have a small circle with radius `r` inside a circle with radius `R`.
The inner circle center can be rotated according to

```
inner_cx = Math.cos(a) * (R - r)
inner_cy = Math.sin(a) * (R - r)
```

We want to figure out how much a point on the inner circle has to be rotated, to cover
arc of the outer circle with angle `a` radians?

So, the inner circle must be rotated by some angle `b` and travel the same distance `s`.

Mathematically,
```
r * b = s
R * a = s   
```

Thus
```
=> r * b = R * a
=> b = (R/r) * a
```

And now we know our inner rotation `b`. Circles are rotated in opposite
directions, so we need to add a minus sign to the final angle: 

```
b = -(R/r) * a
```

## State

The scene is defined as a nested array of circles: 

``` js
{
  // Radius of this spiral, relative to the parent radius.
  radiusRatio: 1, // top level is always 1
  color: 'white',
  children: [{
    // color of the spiral
    color: 'white',
    // Radius relative to parent circle
    radiusRatio: 0.52,
    // where is the hole for a pen relative the radius of this circle
    holeRadius: 0.15,
    // Wher is the hole located inside this circle
    initialAngle: 2.1,
  } 
}
```

Inspired by a Reddit Post that explained the mathematical working behind it and some [desmos graphs](https://www.desmos.com/calculator/cpz4h5fg9e).