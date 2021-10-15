<template>
    <div>
        <input type="text" v-model="msg" @keydown.enter="listAdd">
        <button v-if="mode === 'add'" @click="listAdd">할 일 추가</button>
        <button v-else @click="listAdd">할 일 수정</button>
    </div>
</template>

<script>
import {eventBus} from "../main";

export default {
    // 컴포넌트에서 사용되는 변수선언하기
    data(){
        return{
            // input과 연동될 변수
            msg:"오늘의 할 일을 입력하세요",
            // 순서체크 변수
            index:null,
            // 데이터의 상태체크 변수
            mode:"add"
        }
    },
    created(){
        // this vue객체
        var vm = this;
        eventBus.$on("listEditE",function(pmsg,pindex){
            // this eventBus
            // console.log(pmsg,pindex,this);
            vm.msg=pmsg;
            vm.index=pindex;
            vm.mode="edit";
        })
    },
    methods:{
        //할일 추가할 때 실행할 함수
        listAdd(){
            if(this.msg !== null){
                if(this.mode==="add"){
                    // 보내기(이벤트이름,보낼데이터)
                    this.$emit("listAddE",this.msg);
                    this.msg=null;
                }
                else{
                    this.$emit("listEditEvent",this.msg,this.index);
                    this.msg=null;
                    this.mode="add";
                }
            }
            
        },
        //할일 수정할 때 실행할 함수
        // listEdit(){
        //     this.$emit("listEditEvent",this.msg,this.index);
        //     this.msg=null;
        //     this.mode="add";
        // }
    }
};

</script>

<style lang="scss" scoped>
    input{
        width:70%;
        font-size: 16px;
        border: 1px solid #ccc;
        line-height: 40px;
        padding: 0 10px;
        border-radius: 30px;
        box-sizing: border-box;
        outline: none;
    }
    button{
        font-size: 15px;
        width: 27%;
        padding:12px;
        border:1px solid transparent;
        border-radius: 30px;
        box-sizing: border-box;
        cursor: pointer;
        color: white;
        background: cornflowerblue;
        margin-left: 3%;
        &:hover{
            background: white;
            color: cornflowerblue;
            border:1px solid cornflowerblue;
        }
    }
</style>