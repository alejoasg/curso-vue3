<script lang="ts">
import { ITodoDto } from "src/dtos/ITodoDto";
import * as vue from "vue";
import ComponentModal from "./ComponentModal.vue";

    export default vue.defineComponent( {
        name : "ComponentList",
                  components:{
            ComponentModal
  
            },  
        beforeCreate(){
            console.log('it is happening a creation');
        },

        emits:["deleteData","save"],
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
  <ul>
    <li title = 'Id' v-on:click="modalShow">  {{todoApp.id}}       </li>
    <li title = 'Name' v-on:click="modalShow">  {{todoApp.name}}     </li>
    <li title = 'Completed' v-on:click="modalShow">  {{todoApp.completed == false?'No(Por Completar)':'Si(Completado)'}}       </li>
     <li title = 'Description' v-on:click="modalShow">  {{todoApp.description}}      </li>
    <li>  <button  title = 'Complete' v-on:click ="completeData"> complete</button> </li>
    <li>  <button title = 'Delete' v-on:click ="deleteRow"> delete </button>     </li>
  </ul>
  <ComponentModal v-if="showModal === true" v-bind:todoApp="todoApp" @close="modalClose"  @save="modalSave"/>

</template>


  
