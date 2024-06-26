<template>
  <!-- interpolation directe dans le template -->
  {{ subTitle }}

  <!-- passage d'un props dans un composant: le nom du props doit être en kebab case par rapport au nom de la variable-->
   <!-- récupération d'un évènement émis par le composant enfant avec @nomDeLEventEmit-->
  <HelloWorld :sub-title="subTitle" :user="user" @update-profession="(profession)=>{display(profession)}" />

  <p>{{ sentence }}</p>

  <!-- lier un input à une variable-->
  <input type="text" v-model="subTitle"> <br>

  <!--récupération des contenus des inputs pour les mettre dans un objet + appel d'une fonction sur l'event input-->
  <input type="text" v-model="user.name" @input="display(user.name)"> <br>
  <input type="text" v-model="user.age"> <br>

  <!--Pour switch de couleur on utilise des classes conditionnelles :class et un event vue @click-->
  <button :class="{'btn-red':isRed, 'btn-blue':!isRed}" @click="() => {isRed=!isRed;} ">switch color</button>

  <HelloWorldSlots>
      <!--Envoi d'un template slot au composant enfant-->
      <template v-slot:name>
        <p :class="{'btn-red':isRed, 'btn-blue':!isRed}">{{ user.name }}</p>
      </template>

      <template v-slot:age>
        <p :class="{'btn-red':isRed, 'btn-blue':!isRed}">{{ user.age }}</p>
      </template>
      
  </HelloWorldSlots>

 
  

</template>

<script setup>
  import HelloWorld from '@/components/helloWorld.vue';
  import HelloWorldSlots from '@/components/helloWorldSlots.vue';
import { computed, watch } from 'vue';
  import {reactive} from 'vue';
  import {ref} from 'vue';

  //ref permet de faire référence directement au dom et se met à jour partout où utilisée quand modifiée
  const subTitle=ref( "La Besse Khoya?");

  //création d'un ojet avec une variable reactive. Les variables reactives ne peuve,t pas être des variables primitives
  const user= reactive({
    name:'Jhonny',
    age:65,
  })

  const isRed= ref(true);

  //Création d'une variable calculée à parti de variables reactives
  const sentence= computed(()=>{
    return "Bonjour, je m'appelle , "+user.name+" et j'ai "+user.age+" ans";
  })

  function display(string){
    console.log(string)
  }

  //Un watcher permet de créer des fonctions prenant en compte l'ancienne et la nouvelle valeur d'une variable reactive
  watch(user, (newValue,oldValue) => {
    console.log("Watch : "+newValue.name+" "+oldValue.name)
  })

  
</script>

<style scoped>

.btn-red{ 
  background-color: red;
}

.btn-blue{
  background-color:blue
}

</style>
