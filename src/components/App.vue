<script lang="ts">

    import { ITodoDto } from "src/dtos/ITodoDto";
import {IUserDto } from "src/dtos/IUserDTO";
import * as vue from "vue";
    import ComponenteH1 from "./ComponenteH1.vue";
    import ComponenteP from "./ComponenteP.vue";
import ComponentTodo from "./ComponentTodo.vue";

    export default vue.defineComponent( {
        name : "App",
     components:{
    ComponenteH1,
    ComponenteP,
    ComponentTodo
},
      data():Record<string,ITodoDto[]> {
        return {
        /*     user1:{
                name :"Alejandro" , 
                surname:"Sanchez",
                age :31
            }, */
            todoApps:[{
                id:1,
                name:'Vue Curse',
                completed:false,
                description:"Curse of framework Vue.js"
            },
            {
               id:2,
                name:'Read More',
                completed:false,
                description:"The goal is read more books"
            },
             {
               id:3,
                name:'Do more sports',
                completed:false,
                description:"Try to do more sports and move the body"
            }]
        }
        },
        created(){
            console.log('it was already created');      
        },
        methods:{

                    changeData(todoAppId:number, data:ITodoDto):void{
                        console.log( this.todoApps[todoAppId]);
                    this.todoApps = this.todoApps.map((item: ITodoDto) => {
                        if (item.id === todoAppId) {
                            item = data;
                            }
                        return item;
                    }); 
                            
                    },
                    deleteData(todoAppId:number):void{
                    this.todoApps = this.todoApps.filter((item: ITodoDto) => item.id !== todoAppId); 
                    }
               }
        }
    ,);

</script>

<template>
    <div>
        <!-- <ComponenteH1/>
        <ComponenteP v-bind:user = user1 /> -->
        <ComponentTodo v-bind:todo-app-array="todoApps"  @deleteData="deleteData"   @save="changeData"/>
    </div>
</template>
