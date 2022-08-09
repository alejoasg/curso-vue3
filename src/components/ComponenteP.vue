<script lang="ts">
import {IUserDto } from "src/dtos/IUserDTO";
import * as vue from "vue";

    export default vue.defineComponent( {
        name : "ComponenteP",
        beforeCreate(){
            console.log('it is happening a creation');

        },
         
        props:{
            user:{
                type: Object as vue.PropType<IUserDto>,
                required: true
            } 
        },
        computed:{
            todoJuntoComputed(){
                let message:string = this.user?.name+"_" + this.user?.surname;
                if(this.cont % 2 !== 0){
                    message = message.split('_').reverse().join("_");
                }
                return message;
            }
        },

        data(){
            return {
                todojunto:"" as string,
                cont:0 as number,
                operationMessage: "" as string
            }
        },

        methods:{
            doLogic(){
                this.todojunto = this.user?.name+"_" + this.user?.surname+"_" + this.user?.age + "_" + Math.random();
            },
            activateCont(){
                this.cont++;
            },
               calculate(operation:string): void {
                const number1:number = Math.floor(Math.random() * 101);
                const number2:number = Math.floor(Math.random() * 101);
                let result:number = 0;
               
               if(operation == 'sum'){
                    result = number1 + number2;
                }else if(operation == 'rest'){
                    result = number1 - number2;
                }
                this.operationMessage = 'Waiting answer for '+ operation + ' of  numbers '+ number1 + ' and '+ number2;
                    
                setTimeout( () => {
                    this.operationMessage = 'the answer is '+ result;
                },2500);
          
            }
        },
         watch:{
            operationMessage(operation:string){
                switch(operation){
                    case 'sum':
                         this.calculate(operation)
                         break;
                         case 'rest':
                             this.calculate(operation)
                              break;
                          
                }
               
            }
         }
    } );

</script>

<template>
    <p>Property Name:{{user?.name}} </p>
    <p>Property SurName:{{user?.surname}} </p>
    <p>Property Age:{{user?.age}}</p>

    <p>Value of TodoJunto: {{todojunto}}</p>
      <button v-on:click="doLogic()">Do Logic clicking</button>
      <br/>
      <br/>
      <button v-on:click="activateCont()">Add cont here</button>
        <p>The cont value is: {{cont}}</p>
    <p>The computed variable is <strong>: {{ todoJuntoComputed }}</strong></p>
     <label> Watcher Operation </label>
     
     <input type="text" name="question" v-model="operationMessage"/>
     <br/>
     <p>{{operationMessage}}</p>
   
</template>