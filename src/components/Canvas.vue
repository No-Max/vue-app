<template>
  <div class="canvas-container" ref="canvasContainer">
    <canvas
      @mousedown="mouseDown"
      @mouseup="mouseUp"
      @mousemove="isPainting && onPaint($event)"
      ref="canvas" />
  </div>
</template>

<script>
export default {
  name: "Canvas",
  props: {
    width: {
      type: Number,
      default: 1,
    },
    color: {
      type: String,
      default: 'black'
    },
  },
  data(){
    return {
      canvas: null,
      context: null,
      isPainting: false,
    };
  },
  mounted() {
    const container = this.$refs.canvasContainer;
    this.canvas = this.$refs.canvas;
    this.canvas.height =  container.clientHeight;
    this.canvas.width = container.clientWidth;
    this.context = this.canvas.getContext('2d');
  },
  methods: {
    mouseDown() {
      this.isPainting = true;
      this.context.beginPath();
    },
    mouseUp() {
      this.isPainting = false;
    },
    onPaint(e) {
      this.context.lineWidth = this.width * 2;
      this.context.strokeStyle = this.color;
      this.context.lineTo(e.layerX, e.layerY);
      this.context.stroke();

      this.context.beginPath();
      this.context.arc(e.layerX, e.layerY, this.width, 0, Math.PI * 2);
      this.context.fillStyle = this.color;
      this.context.fill();

      this.context.beginPath();
      this.context.moveTo(e.layerX, e.layerY);
    }
  },
};
</script>

<style scoped lang="scss">
.canvas-container {
  padding: 0;
  margin: 0;
  height: calc(100vh - 64px);
  width: calc(100vw - 4px);
  border: 2px solid;
}
</style>
