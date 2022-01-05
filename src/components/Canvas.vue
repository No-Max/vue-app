<template>
  <div class="canvas-container" ref="canvasContainer">
    <button class="clear-button" @click="clear">Clear</button>
    <canvas
      @mousedown="mouseDown"
      @mouseup="mouseUp"
      @mousemove="isPainting && onPaint($event)"
      @mouseleave="mouseLeave"
      ref="canvas"
    />
  </div>
</template>

<script>
export default {
  name: "Canvas",
  props: {
    settings: {
      type: Object,
      default: () => ({
        width: 1,
        color: "black",
      }),
    },
  },
  data() {
    return {
      canvas: null,
      context: null,
      isPainting: false,
    };
  },
  mounted() {
    const container = this.$refs.canvasContainer;
    this.canvas = this.$refs.canvas;
    this.canvas.height = container.clientHeight;
    this.canvas.width = container.clientWidth;
    this.context = this.canvas.getContext("2d");
  },
  methods: {
    mouseDown() {
      this.isPainting = true;
      this.context.beginPath();
    },
    mouseUp() {
      this.isPainting = false;
    },
    mouseLeave() {
      this.isPainting = false;
    },
    onPaint(e) {
      this.context.lineWidth = this.settings.width * 2;
      this.context.strokeStyle = this.settings.color;
      this.context.lineTo(e.layerX, e.layerY);
      this.context.stroke();

      this.context.beginPath();
      this.context.arc(e.layerX, e.layerY, this.settings.width, 0, Math.PI * 2);
      this.context.fillStyle = this.settings.color;
      this.context.fill();

      this.context.beginPath();
      this.context.moveTo(e.layerX, e.layerY);
    },
    clear() {
      this.context.fillStyle = "white";
      this.context.fillRect(0, 0, this.canvas.width, this.canvas.height);
      this.context.beginPath();
    },
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
  position: relative;
}
.clear-button {
  position: absolute;
  right: 0;
  top: 0;
}
</style>
