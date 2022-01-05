<template>
  <div class="home">
    <nav id="nav">
      <SettingsPanel @onChange="onSettigsChange" />
    </nav>
    <Canvas :settings="settings" />
  </div>
</template>

<script>
import Canvas from "@/components/Canvas.vue";
import SettingsPanel from "@/components/SettingsPanel.vue";

export default {
  name: "Home",
  components: {
    Canvas,
    SettingsPanel,
  },
  data() {
    return {
      settings: undefined,
    };
  },
  methods: {
    onSettigsChange(settings) {
      this.settings = settings;
    },
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
