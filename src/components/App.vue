<script lang="ts">

    import * as vue from "vue";

    import ComponenteH1 from "./ComponenteH1.vue";
    import ComponenteP  from "./ComponenteP.vue";

    export default vue.defineComponent( {

        name       : "App",
        components : {

            ComponenteH1 : ComponenteH1,
            ComponenteP  : ComponenteP,
        },

        data() {

            return  {

                h1 : "Hello world!!",
                p  : "Good bye",

            };

        },

        methods : {

            /* Ojo con esto, ¡problemas con el this y las funciones arrow!*/
            // click : () {
            /* Una de estas dos es la buena */
            // click : function () {
            doClick() {

                this.h1 =  "Hello world!! " + Math.random();
                this.p =  "Good bye " + Math.random();

            },
        },

    } );

</script>

<template>

    <div>

        <p>Cambia el valor para el h1 y el p<button v-on:click="doClick()">Click</button></p>

        <ComponenteH1 text="Hello world!!" />
        <ComponenteP text="Good bye"> </ComponenteP>

        <ComponenteH1 v-bind:text="h1" />
        <ComponenteP v-bind:text="p"> </ComponenteP>

    </div>

</template>
