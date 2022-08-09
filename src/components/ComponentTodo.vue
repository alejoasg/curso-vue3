<script lang="ts">
import { ITodoDto } from "src/dtos/ITodoDto";
import * as vue from "vue";
import ComponentTodoTable from "./ComponentTodoTable.vue";
import ComponentList from "./ComponentList.vue";

    export default vue.defineComponent( {
        name : "ComponentTodo",
             components:{
    ComponentTodoTable,
    ComponentList
  
},

   data (): Record<string, unknown>  {
            return {
            theRadio: "",
            todoappVar:{
                type: Object as vue.PropType<ITodoDto>,
                required: true
            } 
        };
        },
        
        beforeCreate(){
            console.log('it is happening a creation');

        },
        emits:["deleteData","save"],
        props:{
            todoAppArray:{
                type: Array as vue.PropType<ITodoDto[]>,
                required: true
            } 
        },
        methods:{
                deleteData(id:number): void { 
                        this.$emit("deleteData",id);
                },
                save(id:number,data:ITodoDto): void {
                        this.$emit("save",id,data);
                }
        }
    } );

</script>
<template>
<input type="radio" id="one" value="List" v-model="theRadio" />
<label for="one"> List </label> 
<input type="radio" id="two" value="Table" v-model="theRadio" />
<label for="two"> Table </label> 
<span>Picked: {{ theRadio }}</span>

<h1>Aplicacion de Todos</h1>

<ComponentTodoTable  v-if="theRadio === 'Table'" v-bind:todo-app-array ="todoAppArray" @save="save" @deleteData="deleteData"/>
  
<ComponentList  v-if="theRadio === 'List'" v-for="todoApp in todoAppArray"  v-bind:key="todoApp.id" 
 v-bind:todo-app="todoApp" @save="save" @deleteData="deleteData" />

</template>


  
