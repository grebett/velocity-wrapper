#Definition
Basic wrapper for velocity (https://github.com/julianshapiro/velocity) by grebett.
It enables you to create reusable effects such as:

```javascript
var effect = {
  css: {
    y: '-=200px',
    cy: '-=200px'
  },
  options: {
    easing: 'linear',
    duration: 200
  }
};
```

or array of effects like:

```javascript
var arrayOfEffects = [{
  css: {
    x: '+=200px',
    cx: '+=200px'
  },
  options: {
    easing: 'linear',
    duration: 200
  }
}, {
  css: {
    y: '+=100px',
    cy: '+=100px'
  },
  options: {
    easing: 'linear',
    duration: 200
  }
}];
```

#Dependencies
Dependencies needed:

* __lodash__: http://lodash.com/
* __jQuery__: http://jquery.com/download/

#Usages

Considering a rect and a circle as below:
```javascript
var $rect = $('rect'),
    $circle = $('circle');
```

Basic velocity call: 
```javascript
velocity($rect, effect);
```

Overwriting call:
```javascript
velocity($rect, effect, {duration:1000});
```

Predefined string effect call:
```javascript
velocity($rect, 'fadeOut');
```

Velocity accepts an effect composed of an array of step:
```javascript
velocity($rect, arrayOfEffects);
```

Or an array of effects:
```javascript
velocity($rect, [effect1, effect2, effect1, 'fadeOut']);
```

Each effect in the array can be overwritten passing the array `[effect, overwriting options]`:
```javascript
velocity($rect, [effect1, [effect1, {duration: 1000}], effect2]);
```

If you want to conserve last overwriting effect options, use `=`:
```javascript
velocity($rect, [effect1, [effect1, {duration:1000}], [effect2, '=']]);
```

You can start another animation easily using the complete attribute:
```javascript
var startCircleAnimation = function () {
    velocity($circle, [effect1, [effect1, {duration: 1000}], S]);
};
velocity($rect, [effect1, effect1, [effect3, {complete: startCircleAnimation}], 'fadeOut']);
```

Combining these possibilities, you can easily combine effects into a reusable animation:
```javascript
var startSquareAnimation = function () {
    velocity($rect, e0);
};
var startCircleAnimation = function () {
    velocity($circle, e1);
};
var e0 = [effect0, effect1, [effect2, {complete: startCircleAnimation}]];
var e1 = [effect0, effect1, [effect2, {complete: startSquareAnimation}]];
```
