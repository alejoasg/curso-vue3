<script lang="ts">
import { ITodoDto } from "src/dtos/ITodoDto";
import * as vue from "vue";

    export default vue.defineComponent( {
        name : "ComponentModal",
        emits:['close','save'],
           props:{
            todoApp:{
                type: Object as vue.PropType<ITodoDto>,
                required: true
            } 
        },
    
        data:():Record<string, unknown> => {
            return {
                todoAppData :{
                type: Object as vue.PropType<ITodoDto>,
                required: true
            }  ,
                name:{
                type: String,
                required: true
            } ,
             description:{
                type: String,
                required: true
            } ,
            checkboxRed:false,
            checkboxBlack:false
            }
        },
        beforeMount(){
          this.name =this.todoApp.name;
          this.description =this.todoApp.description;
          
        },
        mounted(){
          this.$refs.input_description.focus();
        },

        methods:{
                saveChanges() : void {
                    this.todoAppData = this.todoApp;
                    this.todoAppData.name = this.$refs.input_name.value;
                    this.todoAppData.description = this.$refs.input_description.value;
                    this.$emit("save",this.todoApp.id,this.todoAppData);
                },

                 close() : void {
                    this.$emit("close");
                },

              checkboxRedLetter() : void {
                  if(this.checkboxRed === true){
                    this.$refs.label_name.style.color= "red";
                    this.$refs.label_description.style.color ="red";
                  } else {
                    this.$refs.label_name.style.color="black";
                    this.$refs.label_description.style.color="black";
                  }
                },
                checkboxBlackLetter() : void {
                 if(this.checkboxBlack === true){
                    this.$refs.label_name.style.fontWeight = "bold";
                   this.$refs.label_description.style.fontWeight = "bold";
                  } else {
                    this.$refs.label_name.style.fontWeight = "normal";
                    this.$refs.label_description.style.fontWeight = "normal";
                  }

                },
        }
    } );

</script>
<template>
  <div class="modal-backdrop">
    <div class="modal">
        <slot name="header">
          <header>Header By Default</header>
        </slot>
     <section class="modal-body">
      <input type="checkbox" v-model="checkboxRed" @change="checkboxRedLetter" />
      <label for="checkbox">Red Label</label>
       <input type="checkbox" v-model="checkboxBlack" @change="checkboxBlackLetter" />
      <label for="checkbox">Black Letter Label</label>
      <form>
        <label ref = "label_name"> Name </label>
        <input type="text"  id="name" ref = "input_name" v-model="name"> <br/>
         <label ref = "label_description"> Description </label>
         <input type="text" id="description" ref = "input_description" v-model="description"><br/>
        <slot name="footer">
          <header>Footer By Default</header>
        </slot>
        <button type="button"  class="btn-green" @click="saveChanges"> Save </button>
        
        <button type="button"  class="btn-green" @click="close"> Close </button>
        </form>
        </section>
    </div>
  </div>
</template>

<style>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    padding: 10px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #4AAE9B;
    border: 2px solid #4AAE9B;
    border-radius: 3px;
  }
</style>


  
