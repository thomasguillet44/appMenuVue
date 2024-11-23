<template>
    <div class="central-menu-container">
        <h2 ref="editableName" contenteditable="true">{{ menu.nom }}</h2>

        <p ref="editableEntree" contenteditable="true">{{ menu.entree.nom }}</p>
        <p ref="editableEntreeRecette" contenteditable="true">{{ menu.entree.recette }}</p>

        <p ref="editablePlat" contenteditable="true">{{ menu.plat.nom }}</p>
        <p ref="editablePlatRecette" contenteditable="true">{{ menu.plat.recette }}</p>

        <p ref="editableDessert" contenteditable="true">{{ menu.dessert.nom }}</p>
        <p ref="editableDessertRecette" contenteditable="true">{{ menu.dessert.recette }}</p>
    </div>

    <div class="buttons-container">
        <button class="btn btn-success mt-2" @click="save">Save</button>
        <button class="btn btn-secondary mt-2">Télécharger</button>
    </div>
    

    
</template>

<script setup>

    import { ref } from 'vue';    

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

</script>