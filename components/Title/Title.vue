<template>
  <div
    class="main-title"
    :class="[align, { dark: dark }]"
  >
    <p class="caption-title">
      {{ caption }}
    </p>
    <h4>
      {{ text }}
    </h4>
  </div>
</template>

<style lang="scss" scoped>
@import './title-style.scss';
</style>

<script>
export default {
  props: {
    align: {
      type: String,
      default: 'left'
    },
    text: {
      type: String,
      required: true
    },
    caption: {
      type: String,
      required: true
    },
    dark: {
      type: Boolean,
      default: false
    }
  }
}
</script>
