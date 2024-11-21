<!--Partie HTML du single page component
key : pour identifier chaque element de maniere unique, et donc optimiser la reorganisation
le # dans les templates du layout pour remplacer le v-slot, on recuperer ce qu'on envoie dans le layout
via un slot nommé-->
<template>

  <Layout>
    <template #header>
      <h1>Haché Menu</h1>
      <p>User : {{ user }}</p>
      <hr>
    </template>

    <template #aside>
      <input type="text" placeholder="Nom du menu" v-model="nomNouveauMenu">
      <input type="text" placeholder="Entree" v-model="entreeNouveauMenu">
      <input type="text" placeholder="Plat" v-model="platNouveauMenu">
      <input type="text" placeholder="Dessert" v-model="dessertNouveauMenu">
      <button :disabled="nomNouveauMenu.length == 0" @click="addMenu()">Ajouter un menu</button>

      <ul>
        <li v-for="menu in menus" :key="menu.nom">
            <LineMenu :menu="menu" 
              @changeDisplay = "changeDisplay(menu.id)"
              @delete = "deleteMenu(menu.id)"></LineMenu>
        </li>
      </ul>
    </template>

    <template #main></template>

    <template #footer> Footer de l'application</template>


  </Layout>

  
</template>

<!--Partie JS du single page component-->
<script setup>
  
import {ref} from 'vue';
import LineMenu from './LineMenu.vue';
import Layout from './Layout.vue';

  const user = "Thomas-admin";

  const nouveauMenu = ref([]);
  const nomNouveauMenu = ref('');
  const entreeNouveauMenu = ref('');
  const platNouveauMenu = ref('');
  const dessertNouveauMenu = ref('');

  const menus = ref([ {
    id: generateId(),
    toShow: true,
    nom: 'menu1',
    entree: 'entree1',
    plat: 'plat1', 
    dessert: 'dessert1'
  }]);

  const addMenu = () => {

    nouveauMenu.value = {
      id: generateId(),
      toShow: false,
      nom: nomNouveauMenu.value,
      entree: entreeNouveauMenu.value,
      plat: platNouveauMenu.value, 
      dessert: dessertNouveauMenu.value
    }

    menus.value.push(nouveauMenu.value);

    
    nomNouveauMenu.value = ''
    entreeNouveauMenu.value = ''
    platNouveauMenu.value = '' 
    dessertNouveauMenu.value = ''
    nouveauMenu.value = []
  }

  const deleteMenu = (id) => {
    menus.value= menus.value.filter(m => m.id !== id);
  }

  const changeDisplay = (id) => {
    const menuToShow = menus.value.find(m => m.id == id);
    menuToShow.toShow = !menuToShow.toShow;
  }

  function generateId() {
      return Math.floor((1 + Math.random()) * 0x10000)
          .toString(16)
          .substring(1);    
  }
</script>

<!--Partie CSS du single page component-->
<style>
h1 {
  background-color: yellowgreen;
  color: black;
}
</style>

