<template>
  <svg 
    :viewBox="`0 0 ${UNITS} ${UNITS}`" 
    :height="size || '100%'" 
    :width="size || '100%'" 
  >
    <path
      :d="describeArc(UNITS/2, UNITS/2, getRadius(), start, end)" 
      fill="none" 
      :stroke="stroke" 
      :stroke-width="getStrokeWidth(strokeWidth)" 
      :stroke-dasharray="getLengths()"
    />
    <path
      :d="describeArc(UNITS/2, UNITS/2, getRadius(), start, activeEnd())" 
      fill="none" 
      :stroke="activeStroke" 
      :stroke-width="getStrokeWidth(activeWidth)" 
      :stroke-dasharray="getLengths()"
    />
    <text v-bind="this.getTextProps()">{{text}}</text>
  </svg>
</template>

<script>
export default {
  beforeCreate() {
    // Arbitrary dimensions of SVG to set up user-space units
    this.UNITS = 200;
  },
  props: {
    size: {
      type: String,
      default: ''
    },
    text: {
      type: String,
      default: ''      
    },
    textX: {
      type: String,
      default: 'center'
    },
    textY: {
      type: String,
      default: 'center'
    },    
    dashCount: {
      type: Number,
      default: 21
    },
    activeCount: {
      type: Number,
      default: 5
    },
    strokeWidth: {
      type: Number, 
      default: 20
    },
    activeWidth: {
      type: Number, 
      default: 20
    },
    stroke: {
      type: String, 
      default: 'lightgrey'
    },
    activeStroke: {
      type: String,
      default: 'dodgerblue'
    },
    dashSpacing: {
      type: Number,
      default: 1/4
    },
    start: {
      type: Number,
      default: -120
    },
    end: {
      type: Number,
      default: 120
    },
  },
  methods: {
    // Props object for text positioning
    getTextProps(){
      const props = {fill: 'currentColor'};
      if (this.textX == 'center'){
        props['text-anchor']='middle'
        props.x='50%'
      } else if (this.textX == 'right'){
        props['text-anchor']='end'
        props.x='100%' 
      }
      if (this.textY == 'center'){
        props['dominant-baseline']="middle"
        props.y='50%'
      } else if (this.textY == 'bottom'){
        props.y='100%'
      } else {
        props['dominant-baseline']="hanging"
      }
      return props;
    },

    // Stroke is provided as a percentage of the radius, translate into user space units
    getStrokeWidth(stroke){
      return stroke*this.UNITS/200;
    },

    // Determine the 'end' angle of the path for the active dashes in degrees.
    activeEnd(){
      if (this.activeCount == 0){
        return this.start
      }
      return this.start + (this.end-this.start)*(this.activeCount*this.dashPerc() + (this.activeCount-1)*this.spacePerc())
    },

    // An array of the length of the dash & the length of the space between dashes
    getLengths(){
      return [this.getArcLength()*this.dashPerc(), this.getArcLength()*this.spacePerc()]
    },

    // The space beween dashes as a percentage of the total length
    spacePerc(){
      return this.dashSpacing / (this.dashCount-this.dashSpacing);
    },

    // The length of a dash as a percentage of the total length
    dashPerc(){
      return (1-this.dashSpacing) / (this.dashCount-this.dashSpacing);
    },

    // The length of the arc (allowing for negative angles)
    getArcLength(){
      return Math.abs(this.end-this.start)/360 * 2*Math.PI*this.getRadius()
    },

    // Radius of the circle arc
    getRadius(){
      return (this.UNITS-Math.max(this.getStrokeWidth(this.strokeWidth), this.getStrokeWidth(this.activeWidth)))/2
    },

    // SVG path definition requires points in cartesian space
    polarToCartesian(cx, cy, radius, degrees) {
      const radians = (degrees-90) * Math.PI / 180.0;
      return {
        x: cx + (radius * Math.cos(radians)),
        y: cy + (radius * Math.sin(radians))
      };
    },

    // Path definition for circular arc, clockwise when endDegrees
    describeArc(cx, cy, radius, startDegrees, endDegrees){
      const start = this.polarToCartesian(cx, cy, radius, startDegrees);
      const end = this.polarToCartesian(cx, cy, radius, endDegrees);

      let largeArc = (Math.abs(endDegrees-startDegrees) < 180) ? 0 : 1;
      let sweep = (endDegrees < startDegrees) ? 0 : 1;

      return `M${start.x} ${start.y} A${radius} ${radius} 0 ${largeArc} ${sweep} ${end.x} ${end.y}`
    },
  }
}
</script>