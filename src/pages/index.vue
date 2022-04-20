<script setup lang="ts">
import { useUserStore } from '~/stores/user'
import SkelotonBox from '~/components/SkelotonBox.vue'

const user = useUserStore()
const name = $ref(user.savedName)

// const router = useRouter()

const { t } = useI18n()
const isLoading = ref(true)

const reset = () => {
  isLoading.value = true
  timmer(3)
}
function timmer(sec: number) {
  return setTimeout(() => {
    isLoading.value = false
  }, 1000 * sec)
}

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 3000)
})

</script>

<template>
  <div>
    <div text-4xl>
      <div i-carbon-campsite inline-block />
    </div>
    <p>
      <a rel="noreferrer" href="https://github.com/antfu/vitesse" target="_blank">
        Vitesse
      </a>
    </p>
    <SkelotonBox v-if="isLoading" class="rounded-lg my-3" width="60%" bg-color="pink" />
    <h1 v-else>
      我是loading預載動畫  Skeleton Loading Animation
    </h1>
    <p>
      <em text-sm opacity-75>{{ t('intro.desc') }}</em>
    </p>

    <div py-4 />

    <input
      id="input"
      v-model="name"
      :placeholder="t('intro.whats-your-name')"
      :aria-label="t('intro.whats-your-name')"
      type="text"
      autocomplete="false"
      p="x4 y2"
      w="250px"
      text="center"
      bg="transparent"
      border="~ rounded gray-200 dark:gray-700"
      outline="none active:none"
      @keydown.enter="reset"
    >
    <label class="hidden" for="input">{{ t('intro.whats-your-name') }}</label>

    <div>
      <button
        btn m-3 text-sm
        class="cursor-pointer"
        @click="reset"
      >
        reset Loading
        <!-- {{ t('button.go') }} -->
      </button>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
