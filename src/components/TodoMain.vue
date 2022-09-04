<template>
<section class="main">
   <input v-model="isAll" id="toggle-all" class="toggle-all" type="checkbox" />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <!-- 当任务已完成，可以给 li 加上 completed 类，会让元素加上删除线 -->
        <li :class="{completed:item.flag}" v-for="item in list" :key="item.id">
          <div class="view">
            <input class="toggle" type="checkbox" :checked="item.flag" @change="handelChange(item.id,$event)" />
            <label>{{item.title}}</label>
            <button class="destroy" @click="handelDel(item.id)"></button>
          </div>
        </li>
        <!-- <li>
          <div class="view">
            <input class="toggle" type="checkbox" />
            <label>行万里路</label>
            <button class="destroy"></button>
          </div>
        </li> -->
      </ul>
     
  
</section>


</template>

<script>
export default {
props: {
     // 1. 接收渲染的列表数据
     list: {
       type: Array,
       required: true
     }
   },
methods: {
  handelDel(id) {
    this.$emit('deltodo',id)
  },
   handelChange(id,e){
      this.$emit("edittodo",id,e.target.checked)
    }
}, 
computed: {
  isAll: {
    get(){
      return this.list.every(item=>item.flag===true)

    },
    set(newval){
      this.$emit('changeAll',newval)
    }
  }
},  
}
</script>

<style>

</style>