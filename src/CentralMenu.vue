<template>
    <div ref="menuToDownload" class="central-menu-container">
        <h2 ref="editableName" contenteditable="true">{{ menu.nom }}</h2>

        <hr>
        <p class="categorie-menu">Entrée</p>
        <p class="nom-partie-menu" ref="editableEntree" contenteditable="true">{{ menu.entree.nom }}</p>
        <p ref="editableEntreeRecette" contenteditable="true">{{ menu.entree.recette }}</p>

        <hr>

        <p class="categorie-menu">Plat</p>
        <p class="nom-partie-menu" ref="editablePlat" contenteditable="true">{{ menu.plat.nom }}</p>
        <p ref="editablePlatRecette" contenteditable="true">{{ menu.plat.recette }}</p>

        <hr>

        <p class="categorie-menu">Dessert</p>
        <p class="nom-partie-menu" ref="editableDessert" contenteditable="true">{{ menu.dessert.nom }}</p>
        <p ref="editableDessertRecette" contenteditable="true">{{ menu.dessert.recette }}</p>
    </div>

    <div class="buttons-container">
        <button class="btn btn-success mt-2" @click="save">Save</button>
        <button class="btn btn-secondary mt-2" @click="download">Télécharger</button>
    </div>  
</template>

<script setup>

    import { ref } from 'vue';  
    import html2canvas from "html2canvas";  

    const props =defineProps({
        menu: {
            id: String,
            toShow: Boolean,
            nom: String,
            entree: String,
            plat: String, 
            dessert: String
        }
    })

    const editableName = ref(null);

    const editableEntree = ref(null);
    const editableEntreeRecette = ref(null);

    const editablePlat = ref(null);
    const editablePlatRecette = ref(null);

    const editableDessert = ref(null);
    const editableDessertRecette = ref(null);

    const menuToDownload = ref (null);

    const save = () => {
        //ref a chaque champ modifiable pour ensuite les recuperer et les reinjecter dans les propriétés
        //modifie directement la ref parent
        props.menu.nom = editableName.value.innerText;

        props.menu.entree.nom = editableEntree.value.innerText;
        props.menu.entree.recette = editableEntreeRecette.value.innerText;

        props.menu.plat.nom = editablePlat.value.innerText;
        props.menu.plat.recette = editablePlatRecette.value.innerText;

        props.menu.dessert.nom = editableDessert.value.innerText; 
        props.menu.dessert.recette = editableDessertRecette.value.innerText; 
    }

    const download = async () => {
        const toDownload = menuToDownload.value;
        const canvasToDownload = await html2canvas(toDownload);
        const dataURLToDownload = canvasToDownload.toDataURL("image/png");
        const link = document.createElement("a");
        link.href = dataURLToDownload;
        link.download = editableName.value.innerText +".png";
        link.click();
    }

</script>

<style scoped>
.central-menu-container {
    background: bisque;
    border-radius: 20px;
    padding-top: 10px;
    margin-right: 10px;
    margin-left: 10px;
    display: flex;
    align-items: center;
    flex-direction: column;
    border: solid black;
    height: 90%;
}

h2 {
    font-family: "Cormorant Garamond", serif;
    font-weight: 600;
    font-style: normal;
    text-transform: capitalize;
}

p {
    font-size: large;
}

.categorie-menu {
  font-family: "Merriweather", serif;
  font-weight: 900;
  font-style: normal;
}

.categorie-menu:hover {
    cursor: not-allowed !important;
}

.nom-partie-menu {
  font-family: "Merriweather", serif;
  font-weight: 300;
  font-style: italic;
}

.buttons-container {
    margin-left: 10px;
    display: flex;
}

.btn {
    margin-right: 2px;
}

@media screen and (max-height: 446px) {
    .central-menu-container {
        display: flex;
        flex-direction: row;
        align-items: flex-start;
    }
}

</style>