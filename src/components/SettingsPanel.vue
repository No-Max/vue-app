<template>
  <div class="settings-panel">
    <div>
      <label for="color">Color</label>
      <input type="color" id="color" v-model="settings.color" />
    </div>
    <div>
      <label for="width">Width</label>
      <input type="number" id="width" v-model="settings.width" />
    </div>
  </div>
</template>

<script>
export default {
  name: "SettingsPanel",
  data() {
    return {
      settings: {
        color: "#000000",
        width: 1,
      },
    };
  },
  watch: {
    settings: {
      deep: true,
      handler(value) {
        this.$emit("onChange", value);
      },
    },
  },
};
</script>

<style lang="scss">
.settings-panel {
  display: flex;

  & > div {
    padding: 0 5px;
  }
}
</style>
