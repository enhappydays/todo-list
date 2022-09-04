<template>
  <section class="todoapp">
    <!-- 头部部分 -->
    <todo-header 
    @add="handelAdd"
    ></todo-header>
    <!-- 主体部分 -->
    <todo-main 
    :list="filterList"
    @deltodo="handelDelTodo"
    @changeAll="handelChangeAllTodo"
    @edittodo="handelEditTodo"
    ></todo-main>
   

    <!-- 底部部分 -->
    <todo-footer
    :list="list"
    :filterType="filterType"
    @changeFilterType="handelChangeFilterTypetodo"
    @handelRemoveComplated="handelRemoveComplatedTodo"

    ></todo-footer>
   
      
  </section>
</template>

<script>
import  TodoHeader from './components/TodoHeader.vue'
import  TodoMain from './components/TodoMain.vue'
import  TodoFooter from './components/TodoFooter.vue'
export default {
  name:'App',
components:{
  TodoHeader,
  TodoMain,
  TodoFooter
},
data() {
    return {
      // 1. 任务列表数组
      list: JSON.parse(localStorage.getItem('101-todos'))||[],
       filterType:'all'
    }
  },
  methods: {
    handelDelTodo(id) {
      this.list=this.list.filter(item=>item.id !==id)
      // console.log(id)
    },
    handelAdd(title){
   this.list.push({
    id: + new Date(),
    title,
    flag:false
   } )
  },
  handelChangeAllTodo(newVal){
   return this.list.forEach(item => item.flag=newVal)
  },
  handelChangeFilterTypetodo(newType){
    this.filterType=newType
  },
  handelRemoveComplatedTodo(){
    this.list=this.list.filter(item=>item.flag===false)
  },
  handelEditTodo(id,flag){
  const todo = this.list.find(item=>item.id===id)
    todo.flag=flag
  }

  },
  computed:{
   filterList(){
    if (this.filterType==='all') {
      return this.list
    } else if(this.filterType==='active'){
      return this.list.filter(item=>item.flag===false)
    }else{
      return this.list.filter(item=>item.flag===true)
    }
   }
  },
   watch:{
    list:{
      deep:true,
      handler(newValue){
        localStorage.setItem('101-todos',JSON.stringify(newValue))
      }
    }
  }
}
</script>

<style></style>
