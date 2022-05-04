<script setup lang="ts">

const observer: any = ref(null)
const target: any = ref(null)

const emits = defineEmits(['intersect'])
const props = defineProps({
  options: {
    type: Object,
    require: false,
    default: () => {
      return {
        threshold: 0,
        rootMargin: '0px',
        root: null,
      }
    },
  },
  text: {
    type: String,
    default: '',
  },
})

onMounted(() => {
  observer.value = new IntersectionObserver(([entry]) => {
    if (entry && entry.isIntersecting)
      emits('intersect')
  }, props.options)
  observer.value.observe(target.value)
})

onUnmounted(() => {
  observer.disconnect()
})

</script>

<template>
  <div ref="target" class="observer">
    <span v-if="text.length>0">{{ text }}</span>
  </div>
</template>

<style scoped>
.observer {
  width: 100%;
  /* background-color: red; */
  height: 3px;
}
</style>
