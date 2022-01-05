<template>
  <div class="home">
    <nav id="nav">

    </nav>
    <Canvas />
  </div>
</template>

<script>
import Canvas from "@/components/Canvas.vue";

export default {
  name: "Home",
  components: {
    Canvas,
  },
};
</script>

<style lang="scss">
#nav {
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
