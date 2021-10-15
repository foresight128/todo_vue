<template>
    <div>
        <div class="list" v-for="(list,index) in todoListSend" v-bind:key="index">
            <div v-bind:class="{done:list.mode==='done'}">{{list.msg}}</div>
            <div>
                <button v-if="list.mode==='created'" @click="$emit('listDoneE',index,'done')">Done</button>
                <button v-else @click="$emit('listDoneE',index,'created')">Recheck</button>
                <button @click="$emit('listDeleteE',index)">Delete</button>
                <button @click="listEdit(list.msg,index)">Edit</button>
            </div>
        </div>
    </div>
</template>

<script>
import {eventBus} from "../main";
export default {
    props:["todoListSend"],
    methods:{
        listEdit(msg,index){
            eventBus.$emit("listEditE",msg,index)
        }
    }
};
</script>

<style lang="scss" scoped>
    .list{
        border-bottom: 1px solid #ddd;
        margin: 10px;
        padding: 10px;
        box-sizing: border-box;
        >div.done{
            text-decoration: line-through;
            color: #ccc;
        }
        button{
            width: 15%;
            margin: 10px 5px 0 0;
            padding:5px;
            border: 1px solid #ddd;
            border-radius: 30px;
            box-sizing: border-box;
            cursor: pointer;
            &:hover{
                background-color: white;
            }
        }
        
    }
</style>