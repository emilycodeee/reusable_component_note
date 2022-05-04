<script setup lang="ts">
// import { useUserStore } from '~/stores/user'
import SkelotonBox from '~/components/SkelotonBox.vue'
import Observer from '~/components/Observer.vue'

// const user = useUserStore()
// const name = $ref(user.savedName)
const data = [['除了太陽高度', '今晚的寫作還取決於', '天氣狀況、污染、懸浮顆粒物'],
  ['孩子們睡得很好', '孩子們還在密度藍裡游玩', '以後我會教他們算數'],
  ['一朵花加上一朵花等於一朵喇叭花', '一只甲殼蟲减去一只甲殼蟲', '等於一條毛毛蟲'],
  ['我寫作的時候', '心臟是熱的', '和想你的時候一樣'],
  ['所以我想，人類的愛', '肯定保存在太陽的核心之中', '用來維持著太陽系']]

const nav = ['除了', '孩子們', '一朵花', '我寫作', '所以...']
const arr: any = ref([])
let pageNow = 0
const background = 'gray'
// const router = useRouter()

const { t } = useI18n()
const isLoading = ref(true)
const selected = ref('')

const reset = () => {
  isLoading.value = true
  timmer(3)
}
function timmer(sec: number) {
  // console.log(selected.value)
  return setTimeout(() => {
    isLoading.value = false
  }, 500 * sec)

  // console.log(ref)
}

function loadMore() {
  if (pageNow < data.length)
    arr.value = [...arr.value, '', ...data[pageNow]]
  pageNow++
}

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 3000)
})

</script>

<template>
  <ul
    class="fixed z-[9] w-full px-4 flex flex-nowrap gap-4 top-0 py-2
        overflow-x-auto
        bg-white "
  >
    <li v-for="(word,i) in nav" :key="`nav-${i}`" class="min-h-[3.75rem] px-4 flex flex-col items-center justify-center border-2 border-5 " :class="selected.includes(word) && 'border-blue-500/50'">
      {{ word }}
    </li>
  </ul>
  <div>
    <div class="flex items-start">
      <SkelotonBox v-if="isLoading" class="rounded-lg mb-2" width="60%" height="1rem" :bg-color="background" />
      <h1 v-else>
        我是loading預載動畫  Skeleton Loading Animation
      </h1>

      <SkelotonBox v-if="isLoading" class="rounded-lg mb-2" width="100%" height="1rem" :bg-color="background" />
      <p v-else>
        可以傳入寬高與顏色，作為可複用的預載頁面元件，優化使用者體驗。
      </p>
    </div>
    <button
      id="btn"
      btn m-3 text-sm
      class="cursor-pointer"
      @click="reset"
    >
      重設loading時間
      <!-- {{ t('button.go') }} -->
    </button>
    <p>
      畢贛《破碎太陽之心》
      <!-- <em text-sm opacity-75>{{ t('intro.desc') }}</em> -->
    </p>

    <div py-4 />

    <label class="hidden" for="input">{{ t('intro.whats-your-name') }}</label>
    <div v-for="(item,i) in arr" :key="i" class="h-4rem bg-gray ">
      <Observer class="observer" @intersect="selected = item" />
      {{ item }}
    </div>
    <Observer class="observer" text="我也是有底線的好嗎" @intersect="loadMore" />

    <div>
      <button
        id="btn"
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
<style lang="scss">
div{
  display: flex;
  flex-direction: column;
  gap: 10px;
  .test{
  background-color: pink;
  width: 100%;
  height: 1rem;
.observer{
  width: 100%;
  // background-color: red;
  height: 3px;
}
.target {
  width: 100%;
  height: 50px;
  background: red;
}
}}
</style>
<route lang="yaml">
meta:
  layout: home
</route>
