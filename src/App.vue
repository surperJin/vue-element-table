<template>
  <div id="app">
    <table-one></table-one>
    <table-two></table-two>
    <table-three></table-three>
    <p class="m-30">注：这个demo列出稍微复杂的表格样式以及需求，基础的<el-link type="primary" href="https://element.eleme.cn/#/zh-CN/component/table" target="_blank">官网</el-link>都有。demo没有加过多功能（如分页、增删改），这里只为展示需求所用不必深究</p>
  </div>
</template>

<script>
import TableOne from './components/TableOne'
import TableTwo from './components/TableTwo'
import TableThree from './components/TableThree'

export default {
  name: 'App',
  components: {
    TableOne,
    TableTwo,
    TableThree
  }
}
</script>

<style>
</style>
