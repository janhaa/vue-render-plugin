<template lang="pug">
.socket(
  :class="[type, socket.name] | kebab",
  :title="socket.name"
)
</template>

<script>
export default {
  props: ["type", "socket"]
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css?family=Lato&display=swap");

.socket {
  display: inline-block;
  cursor: pointer;
  border: 1px solid white;
  border-radius: 12px;
  width: 24px;
  height: 24px;
  margin: 6px;
  vertical-align: middle;
  background: darkred;
  z-index: 2;
  box-sizing: border-box;

  transition: border-width 0.2s;

  &:hover {
    border-width: 3px;
  }

  &.multiple {
    border-color: yellow;
  }

  &.output {
    margin-right: -12px;
  }

  &.input {
    margin-left: -12px;
  }
}
</style>
