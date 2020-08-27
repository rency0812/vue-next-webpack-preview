<template>
  <div class="root">
    <img src="./logo.png">
    <h1>Hello Vue 3!</h1>
    <p v-for="v in 3" :key="v">{{v}}</p>
    <h4 ref="h4">{{num}}</h4>
    <button @click="inc">Clicked {{ count }} times.</button>
  </div>
</template>

<script>
import { ref, onBeforeMount, watch, watchEffect, reactive, onMounted } from 'vue'

export default {
  setup() {
    const count = ref(0)
    const num = ref(1)
    const datas = reactive({
      name: 'r',
      list: [11,22]
    })
    const inc = () => {
      count.value++
      num.value++
      datas.name += num.value
    }
    const initTem = () => {
      console.log('beforeMount')
    }
    const initEnd = () => {
      console.log('afterMount')
    }
    const h4 = ref(null)

    onBeforeMount(() => {
      initTem()
      initEnd()
    })
    onMounted(() => {
      console.log(h4)
    })

    watchEffect(() => {
      console.log(datas.name)
    })
    watch([count, num], ([val1, val2], [old1, old2]) => {
      console.log(old1, val1)
      console.log(old2, val2)
    })
    watch(() => datas.name, (val, old) => {
      console.log(val, old)
    })

    return {
      count,
      num,
      h4,
      inc
    }
  }
}
</script>

<style scoped>
.root {
  text-align: center;
}
img {
  width: 200px;
}
h1 {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
