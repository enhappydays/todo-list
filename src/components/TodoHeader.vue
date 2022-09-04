<template>
 <header class="header" >
      <h1>todos</h1>
      <input v-model.trim="title" @keyup.enter="Add" class="new-todo" placeholder="请输入任务名称" autofocus />
    </header>
</template>

<script>
export default {
 name:'TodoHeader',
 data(){
  return{
    title:''
  }
},
methods: {
  Add() {
    if (this.title==='') {
    alert('重新写') 
    return
  }
  this.$emit('add',this.title)
  }
},
}
</script>

<style>

</style>