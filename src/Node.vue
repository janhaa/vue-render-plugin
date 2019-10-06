<template lang="pug">
.node(:class="[selected(), node.name] | kebab")
  span.icon
    i.mdi.mdi-24px(:class="'mdi-' + (icon(node.name) || 'link')")
  .title {{node.name}}

  // Outputs
  .outputSocket(v-for='output in outputs()' :key="output.key")
    .output-title {{output.name}}
    Socket(v-socket:output="output", type="output", :socket="output.socket")

  // Controls
  .controlSocket(
    v-for='control in controls()',
    v-control="control"
  )

  // Inputs
  .inputSocket(v-for='input in inputs()' :key="input.key")
    Socket(v-socket:input="input", type="input", :socket="input.socket")
    .input-title(v-show='!input.showControl()') {{input.name}}
    .input-control(
      v-show='input.showControl()'
      v-control="input.control"
    )
</template>

<script>
import mixin from "./mixin";
import Socket from "./Socket.vue";

export default {
  mixins: [mixin],
  components: {
    Socket
  }
};
</script>

<style lang="scss" scoped>
$background-color: #4a4a4a;
$selected-background-color: #7957d5;
$hover-background-color: darken(#4a4a4a, 10%);

@import url("https://fonts.googleapis.com/css?family=Lato&display=swap");

.icon {
  float: left;
  color: white;
  margin: 6px;
}

.node {
  background: $background-color;
  border: 3px solid;
  background-color: lighten($background-color, 5%);
  border-radius: 3px;
  cursor: pointer;
  min-width: 180px;
  height: auto;
  padding-bottom: 6px;
  box-sizing: content-box;
  position: relative;
  user-select: none;
  margin-bottom: 0;

  &:hover {
    background-color: $hover-background-color;
    border-color: lighten($hover-background-color, 5%);
    color: #363636;
  }

  // &.selected {
  //   background-color: $selected-background-color;
  //   border-color: lighten($selected-background-color, 5%);
  // }

  .title {
    color: white;
    font-family: "Lato", sans-serif;
    font-size: 18px;
    padding: 8px;
  }

  .outputSocket {
    text-align: right;
  }

  .inputSocket {
    text-align: left;
  }

  .input-title,
  .output-title {
    vertical-align: middle;
    color: white;
    display: inline-block;
    font-family: "Lato", sans-serif;
    font-size: 18px;
    margin: 6px;
    line-height: 24px;
  }

  .input-control {
    z-index: 1;
    width: calc(100% - 36px);
    vertical-align: middle;
    display: inline-block;
  }

  .control {
    padding: 6px 18px;
  }

  .controlSocket {
    padding: 5px;
  }
}
</style>