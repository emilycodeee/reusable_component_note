<script setup lang="ts">

const props = defineProps({
  maxWidth: {
    // The default maxiumum width is 100%.
    default: 100,
    type: Number,
  },
  minWidth: {
    // Lines have a minimum width of 80%.
    default: 80,
    type: Number,
  },
  height: {
    // Make lines the same height as text.
    default: '1em',
    type: String,
  },
  width: {
    // Make it possible to define a fixed
    // width instead of using a random one.
    default: null,
    type: String,
  },
  bgColor: {
    default: '#DDDBDD',
    type: String,
  },
})
const computedWidth = computed(() => {
  // Either use the given fixed width or
  // a random width between the given min
  // and max values.
  return props.width || `${Math.floor((Math.random() * (props.maxWidth - props.minWidth)) + props.minWidth)}%`
})

</script>

<template>
  <span
    :style="{ height:props.height, width: computedWidth ,backgroundColor:props.bgColor}"
    class="SkeletonBox"
  />
</template>

<style lang="scss" scoped>
 .SkeletonBox {
  display: inline-block;
  position: relative;
  overflow: hidden;
  vertical-align: middle;
//   background-color: #DDDBDD;

  &::after {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    transform: translateX(-100%);
    background-image: linear-gradient(
      90deg,
      rgba(#fff, 0) 0,
      rgba(#fff, 0.2) 20%,
      rgba(#fff, 0.5) 60%,
      rgba(#fff, 0)
    );
    animation: shimmer 5s infinite;
    content: '';
  }

  @keyframes shimmer {
    100% {
      transform: translateX(100%);
    }
  }
}

</style>
