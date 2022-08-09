<script lang="ts">

    import * as vue from "vue";

    export default vue.defineComponent( {
        name : "ComponenteH1",
        beforeCreate(){
            console.log('it is happening a creation');
        },
        created(){
            console.log('it was already created');
        }
    } );

</script>

<template>
    <h1>
        Hello Alejandro,yeah H1
    </h1>
</template>
