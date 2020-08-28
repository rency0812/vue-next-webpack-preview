<template>
  <div class="root">
    <img src="./logo.png">
    <h1>Hello Vue 3!</h1>
    <p v-for="v in 3" :key="v">{{v}}</p>
    <h4 ref="h4">{{num}}</h4>
    <input type="text" v-model="count">
    <button @click="inc">Clicked {{ count }} times.</button>
    <Child @childEvent="childEvent"/>
  </div>
</template>

<script>
import { ref, onBeforeMount, watch, watchEffect, reactive, onMounted } from 'vue'
import Child from './compents/Child.vue'
import axios from 'axios'

export default {
  components: {
    Child
  },
  emits: {
    childEvent (val) {
      console.log(val)
      return true
    }
  },
  setup(props, context) {
    // const formData = new FormData()
    const formData = 'name=renl'
    // formData.append('name', 'renl')
    axios({
      url: '/user/12345',
      method: 'post',
      data: formData
    })
    console.log(context)
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

    const childEvent = (val) => {
      console.log(val)
      return true
    }

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
      childEvent,
      inc
    }
  }
}
</script>

<style lang="less" scoped>
.root {
  text-align: center;
  button{
    box-shadow: 0 0 3px #000;
  }
}
img {
  width: 200px;
}
h1 {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
