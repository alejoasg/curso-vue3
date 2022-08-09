<script lang="ts">
import { ITodoDto } from "src/dtos/ITodoDto";
import * as vue from "vue";
import ComponentRow from "./ComponentRow.vue";
import ComponentList from "./ComponentList.vue";

    export default vue.defineComponent( {
        name : "ComponentTodoList",
             components:{
    ComponentRow,
    ComponentList,
  
},

   data :():Record<string, unknown>  => {
            return {
            theRadio: ""
        };
        },
        emits:["deleteData","save","modalData"],
        props:{
            todoAppArray:{
                type: Array as vue.PropType<ITodoDto[]>,
                required: true
            } 
        },
        methods:{
                    deleteData(id:number){
                        console.log('test'+ id);
                        this.$emit("deleteData",id);
                },
                   save(id:number,data:ITodoDto){
                        console.log('test'+ id);
                        this.$emit("save",id,data);
                },
                  modalData(data:ITodoDto) :void {
                     this.$emit("modalData",data);
                }
        }
    } );

</script>
<template>
<table>
    <thead>
<tr>
  <td><strong> Id </strong>       </td>
  <td><strong> Name  </strong>    </td>
  <td><strong> Completed </strong></td>
  <td><strong> Description </strong></td>
  <td><strong> Complete </strong></td>
  <td><strong> Delete </strong></td>
</tr>
    </thead>
<ComponentRow v-for="todoApp in todoAppArray"  v-bind:key="todoApp.id" v-bind:todo-app="todoApp" @modalData="modalData" @deleteData="deleteData" @save="save" />
  </table>
</template>



  
