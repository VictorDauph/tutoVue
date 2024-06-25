<template>
    <h1>Wesh!</h1>
    <p>{{props.subTitle}}</p>
    <p>
        {{ props.user.name }} 
        <!-- affichage conditonnel de blocs en fonction d'une variable réactive-->
        <span v-if="props.user.age>=18">
            {{ props.user.age }} 
        </span> 
        <span v-else>
            La personne est mineure
        </span> 
    </p>

    <!--récupération d'un event pour envoi au composant parent-->
    <input type="text" v-model="profession" @input="handleUpdate">
  </template>
  

  <script setup>
    import { ref } from 'vue';


    //Récupération de props depuis le composant parent  
    const props = defineProps(['subTitle','user']);

    const profession= ref("artisan");

    //création d'un évènement que l'on peut émettre vers le composant parent
    const emit=defineEmits(['updateProfession']);

    //Fonction d'envoi d'une valeur au composant parent
    function handleUpdate(event){
      emit('updateProfession', event.target.value);
    }
  </script>
  
  <style scoped>
    h1{ 
      color: red;
    }
    p{ 
      color: red;
    }
  </style>
  