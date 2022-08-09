<script lang="ts">
import { ITodoDto } from "src/dtos/ITodoDto";
import * as vue from "vue";
import ComponentModal from "./ComponentModal.vue";

    export default vue.defineComponent( {
        name : "ComponentRow",
                components:{
            ComponentModal
  
            },
        beforeCreate(){
            console.log('it is happening a creation');
        },

        emits:["deleteData", "save","modalData"],
        props:{
            todoApp:{
                type: Object as vue.PropType<ITodoDto>,
                required: true
            } 
        },
             data (): Record<string, unknown>  {
            return {
                showModal: false,   
            }

        },
        methods:{
                completeData() : void {
                        let data:ITodoDto = this.todoApp;
                                data.completed = true;
                        this.$emit("save",this.todoApp.id,data);
                },
                deleteRow() : void {
                    this.$emit("deleteData",this.todoApp.id);
                },
                modalShow() : void {
                        this.showModal = true;
                },
                modalSave(id:number,data:ITodoDto): void {
                        this.showModal = false;
                        this.$emit("save",this.todoApp.id,data);
                },
                modalClose(): void {
                        this.showModal = false;
                }
        }
    } );

</script>
<template>
<tr>
    <td title = 'Id' v-on:click="modalShow" >  {{todoApp.id}}       </td>
    <td title = 'Name' v-on:click="modalShow" >  {{todoApp.name}}     </td>
    <td title = 'Completed' v-on:click="modalShow">  {{todoApp.completed == false?'No(Por Completar)':'Si(Completado)'}}       </td>
    <td title = 'Description' v-on:click="modalShow">  {{todoApp.description}}     </td>
    <td>  <button title="complete" v-on:click ="completeData"> complete</button> </td>
    <td>  <button title="delete" v-on:click ="deleteRow"> delete </button>     </td>
  </tr>
   <ComponentModal v-if="showModal === true" v-bind:todoApp="todoApp" @close="modalClose"  @save="modalSave"/>
</template>


  
