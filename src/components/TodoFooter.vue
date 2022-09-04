<template>
<footer class="footer" v-if="list.length>0">
      <span class="todo-count"><strong>{{leftcount}}</strong>剩余</span>
      <ul class="filters">
        <li>
          <a 
          :class="{selected: filterType === 'all'}" 
          href="#/"
          @click.prevent="changeFilterType('all')"
          >全部</a>
        </li>
        <li>
          <a 
          :class="{selected: filterType === 'active'}" 
          href="#/active"
          @click.prevent="changeFilterType('active')"
          >进行中</a>
        </li>
        <li>
          <a 
          :class="{selected: filterType === 'completed'}" 
          href="#/completed"
          @click.prevent="changeFilterType('completed')"
          >
          已完成</a>
        </li>
      </ul>
      <button class="clear-completed" @click="handelRemove">清除已完成</button>
    </footer>
 
   

</template>

<script>
export default {
  name:'TodoFooter',
props: {
     // 1. 任务列表
     list: {
       type: Array,
       required: true
     },
     filterType: {
      type:String,
      required:true
     }
   },
   computed: {
    leftcount() {
      return  this.list.filter(item => item.flag === false).length 
    }
   },
   methods: {
    changeFilterType(newType) {
      this.$emit('changeFilterType',newType)
    },
    handelRemove(){
      this.$emit('handelRemoveComplated')
    }
   },
}
</script>

<style>

</style>