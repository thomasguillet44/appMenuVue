<!--Partie HTML du single page component
key : pour identifier chaque element de maniere unique, et donc optimiser la reorganisation
le # dans les templates du layout pour remplacer le v-slot, on recuperer ce qu'on envoie dans le layout
via un slot nommé-->
<template>

  <ModaleAdd :visible="modaleAddIsVisible"
            @close="closeModale"
            @addMenu="addMenu"></ModaleAdd>

  <Layout>
    <template #header>
      <h1>Haché Menu</h1>
      <p>User : {{ user }}</p> 
      <div class="btn btn-secondary m-2" @click="showModalAddMenu()">Ajouter un menu</div>
      <hr>
    </template>

    <template #aside>      
      <div class="overflow-list">
        <ul>
          <li v-for="menu in menus" :key="menu.nom">
            <LineMenu :menu="menu" 
              @changeDisplay = "changeDisplay(menu)"
              @delete = "deleteMenu(menu.id)"
              @modify="modifyMenuOnCentralPanel(menu.id)"
              @showEntree="changeDisplay(menu.entree)"
              @showPlat="changeDisplay(menu.plat)"
              @showDessert="changeDisplay(menu.dessert)"></LineMenu>
          </li>
        </ul>
      </div>     
    </template>

    <template #main>
      <div v-if="hasMenuOnCentralPanel">
        <CentralMenu :menu="menuToDisplayOnCentralPanel"></CentralMenu>
      </div>
    </template>

    <template #footer> Footer de l'application</template>
  </Layout>

  
</template>

<!--Partie JS du single page component-->
<script setup>
  
import {ref, watchEffect} from 'vue';

import LineMenu from './LineMenu.vue';
import Layout from './Layout.vue';
import CentralMenu from './CentralMenu.vue';
import ModaleAdd from './ModaleAdd.vue';

  const user = "Thomas-admin";

  const menus = ref([ {
    id: generateId(),
    toShow: true,
    nom: 'menu1',
    entree: {nom: "entree1", recette: "recette de l'entree"},
    plat: {nom: "plat1", recette: "recette du plat"}, 
    dessert: {nom: "dessert1", recette: "recette du dessert"}
  }]);

  const menuToDisplayOnCentralPanel = ref ([]);

  const hasMenuOnCentralPanel = ref(false);

  const modaleAddIsVisible = ref(false);

  watchEffect(() => {
    hasMenuOnCentralPanel.value = menuToDisplayOnCentralPanel.value.id != null;
  })

  const showModalAddMenu = () => {
    modaleAddIsVisible.value = true;
  }

  //on est obligé de créer un nouveau menu et de le créer a partir des propriétés récupérées, 
  //car les objets ne correspondent pas exactement
  //par ailleurs on doit faire cette petite opération avec les json car sinon je n'arrive pas a avoir 
  //acces au valeur du proxy
  const addMenu = (nouveauMenuToSend) => {

    const stringObject = JSON.stringify(nouveauMenuToSend);
    const jsonParsedObject = JSON.parse(stringObject);

    const nom = jsonParsedObject.nouveauMenuToSend.nom;
    const entree = jsonParsedObject.nouveauMenuToSend.entree;
    const plat = jsonParsedObject.nouveauMenuToSend.plat;
    const dessert = jsonParsedObject.nouveauMenuToSend.dessert;

    const menuToAdd = {
      id: generateId(),
      toShow: true,
      nom: nom,
      entree: {nom: entree, recette: "recette de l'entree", toShow: false},
      plat: {nom: plat, recette: "recette du plat", toShow: false}, 
      dessert: {nom: dessert, recette: "recette du dessert", toShow: false}
    }

    menus.value.push(menuToAdd);
  }

  const deleteMenu = (id) => {
    menus.value= menus.value.filter(m => m.id !== id);
    if (id == menuToDisplayOnCentralPanel.value.id) {
      menuToDisplayOnCentralPanel.value = [];
    }
  }

  const changeDisplay = (elem) => {
    elem.toShow = !elem.toShow;
  }

  const modifyMenuOnCentralPanel = (id) => {
    menuToDisplayOnCentralPanel.value = findMenuInMenus(id);
  }

  const closeModale = () => {
    modaleAddIsVisible.value = !modaleAddIsVisible;
  }

  function findMenuInMenus(id) {
    return menus.value.find(m => m.id == id);
  }

  function generateId() {
      return Math.floor((1 + Math.random()) * 0x10000)
          .toString(16)
          .substring(1);    
  }

</script>

<!--Partie CSS du single page component-->
<style>


</style>

