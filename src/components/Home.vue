<template>
    <div class="wrap">
        <h1>TODAY TODOS</h1>
        <p>
            <strong> All : {{todoList.length}}</strong>  / 
            <strong> COMPLETE : {{countDone}}</strong>  / 
            <strong> DONE : {{todoList.length - countDone}}</strong>
        </p>
        <div>
            <!-- 이벤트버스로 보낸 이벤트(listAddE) 실행할 때 listAdd실행 -->
            <ListAdd @listAddE = "listAdd" @listEditEvent = "listEdit"></ListAdd>
            <List v-bind:todoListSend="todoList" @listDeleteE = "listDelete" @listDoneE = "listDone"></List>
        </div>
    </div>
</template>

<script>
import ListAdd from './ListAdd.vue';
import List from './List.vue';

var STORAGE_KEY = "todos-vuejs";
var todoStorage = {
  fetch: function () {
    var todoList = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
    todoList.forEach(function (todo, index) {
      todo.id = index;
    });
    todoStorage.uid = todoList.length;
    return todoList;
  },
  save: function (todoList) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todoList));
  },
};


export default {
    components:{
        ListAdd,
        List
    },
    data(){
        return{
            // 할일을 저장할 배열
            todoList: todoStorage.fetch(),
        }
    },
    watch: {
        todoList: {
            handler: function (todoList) {
                todoStorage.save(todoList);
            },
            deep: true,
        }
    },

    computed:{
        countDone(){
            var count = 0;
            this.todoList.forEach(function(list){
                if(list.mode === "done") count++;
            });
            return count;
        }
    },
    methods:{
        listAdd(msg){
            // console.log("오케이"+msg);
            // todoList 배열 끝에 추가
            this.todoList.push({msg:msg,mode:"created"})
        },
        listDelete(index){
            this.todoList.splice(index,1)
        },
        listDone(index,pmode){
            this.todoList[index].mode=pmode
        },
        listEdit(pmsg,pindex){
            this.todoList[pindex].msg=pmsg;
            // this.todoList[pindex].mode=pmode;
        }

    }
};
</script>

<style lang="scss" scoped>
// 얘를 부른 App.vue에서도 스타일 쓸수 있도록 사용 - scoped
    .wrap{
        width: 600px;
        margin: 50px auto 0;
        background: white;
        padding: 20px;
        box-sizing: border-box;
        border-radius: 20px;
        box-shadow: 0 0 4px rgba(0,0,0,0.3);
        font-size: 14px;
        color: #333;
        h1{
            text-align: center;
            margin: 15px 0;
        }
        p{
            margin: 0 5px 10px;
        }
    }
    
</style>