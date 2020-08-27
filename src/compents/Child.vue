<template>
  <div>this is child</div>
</template>
<script>
export default {
  setup (props, context) {
    context.emit('childEvent', '孩子from child')
    return {}
  }
}
</script>
<style lang="less" scoped>
</style>
