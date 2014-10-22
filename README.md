#Definition
Basic wrapper for velocity (https://github.com/julianshapiro/velocity) by grebett.
Enables create reusable effects such as:

`var effect = {
  css: {
    y: '-=200px',
    cy: '-=200px'
  },
  options: {
    easing: 'linear',
    duration: 200
  }
};`

or array of effects like:

`var arrayOfEffects = [{
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
}];`

#Dependencies
Dependencies needed:
* __lodash__: http://lodash.com/
* __jQuery__: http://jquery.com/download/

#Examples

Considering a rect and a circle as below:
`var $rect = $('rect'),
    $circle = $('circle');`

Basic velocity call: 
`velocity($rect, N);`

Overwriting call:
`velocity($rect, N, {duration:1000});`

Predefined string effect call:
`velocity($rect, 'fadeOut');`

Velocity accepts an effect composed of an array of step:
`velocity($rect, arrayOfEffects);`

Or an array of effects:
`velocity($rect, [S, S, N, 'fadeOut']);`

Each effect in the array can be overwritten passing the array `[effect, overwriting options]`:
`velocity($rect, [S, [N, {duration: 1000}], S]);`

If you want to conserve last overwriting effect options, use '=':
`velocity($rect, [S, [N, {duration:1000}], [S, '=']]);`

You can start another animation easily using the complete attribute:
`var startCircleAnimation = function () {
    velocity($circle, [S, [N, {duration: 1000}], S]);
};
velocity($rect, [S, S, [N, {complete: startCircleAnimation}], 'fadeOut']);`

You can easily combine effects into a reusable animation:
`var startSquareAnimation = function () {
    velocity($rect, e0);
};
var startCircleAnimation = function () {
    velocity($circle, e1);
};
var e0 = [S, S, [N, {complete: startCircleAnimation}]];
var e1 = [S, S, [N, {complete: startSquareAnimation}]];
`
