<template>  
    <!--affichage du template slot envoyé par le parent-->
    <slot name="name"></slot>
    <slot name="age"></slot>
</template>


<script setup>

</script>

<style scoped>
h1{ 
    color: blue;
}
p{ 
    color: blue;
}
</style>
