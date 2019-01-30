<template>
    <div id="app">
        <div id="cover"></div>
        <vHeader></vHeader>
        <vTodo></vTodo>
        <vFooter></vFooter>
    </div>
</template>

<script>
import vHeader from './todo/header.vue'
import vFooter from './todo/footer.jsx'
import vTodo from './todo/todo.vue'

export default {
  components: {
      vHeader,
      vFooter,
      vTodo,
  }
}
</script>

<style lang="stylus" scoped>
#app
    position absolute 
    left 0
    right 0
    top 0
    bottom 0
    #cover
        position absolute
        left 0
        right 0
        top 0
        bottom 0
        background-color #999 
        opacity .1
        z-index -1
</style>

