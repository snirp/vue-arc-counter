<template>
  <svg :viewBox="`0 0 ${UNITS} ${UNITS}`" height="100%" width="100%">
    <path
      :d="describeArc(UNITS/2, UNITS/2, getRadius(), start, end)" 
      fill="none" 
      :stroke="stroke" 
      :stroke-width="getStrokeWidth()" 
      :stroke-dasharray="getLengths()"
    />
    <path
      :d="describeArc(UNITS/2, UNITS/2, getRadius(), start, activeEnd())" 
      fill="none" 
      :stroke="activeStroke" 
      :stroke-width="getStrokeWidth()" 
      :stroke-dasharray="getLengths()"
    /> 
  </svg>
</template>

<script>
export default {
  beforeCreate() {
    // Arbitrary dimensions of SVG to set up user-space units
    this.UNITS = 32;
  },
  props: {
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
    // Stroke is provided as a percentage of the radius, translate into user space units
    getStrokeWidth(){
      return this.strokeWidth*this.UNITS/200;
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
      return (this.UNITS-this.getStrokeWidth())/2
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