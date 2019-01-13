# VUE ARC COUNTER

This Vue component generates counter in a circular arc. The angles, colors, strokewidth, spacing between dashes and 
direction can all be controlled through properties.

## Examples

![diagram of vue-polar](https://raw.githubusercontent.com/snirp/vue-arc-counter/master/examples.png)

[Sample code on codesandbox](https://codesandbox.io/s/github/snirp/vue-arc-counter)

## Project setup

With a package manager
```
# npm
$ npm install vue-arc-counter

#yarn
$ yarn add vue-arc-counter
```

For the browser
```
<script src="unpkg.com/vue-arc-counter@latest/dist/arcCounter.umd.min.js"></script>
```

## How it works
The component generates an `SVG` element with default width and height of 100% (outer diameter of the counter).
Two dashed strokes are overlayed: the bottom one controlled by `stroke` and `dashCount` and the top one by 
`activeStroke` and `activeCount`. A `start` angle smaller than the `end` angle will make for clockwise counting, 
vice versa.

The absolute difference between `end` and `start` angles should always be less than 360 degrees.

## Properties
|prop|description|default|options|
|:---|---|---|---|
|`dashCount`|Total number of dashes|`21`|Natural number|
|`activeCount`|Number of dashes on top|`5`|Natural number|
|`strokeWidth`|Stroke as a percentage of the radius|`20`|`0` to `100`|
|`stroke`|Stroke color of the bottom dashes|`lightgrey`|`color`|
|`activeStroke`|Stroke color of the top dashes|`dodgerblue`|`color`|
|`dashSpacing`|Fraction of width taken up by space between dashes|`1/4`|`0` to `1`|
|`start`|Start angle from top|`-120`|`-360` to `360`|
|`end`|End angle from top|`120`|`-360` to `360`|

## License

MIT Open Source License