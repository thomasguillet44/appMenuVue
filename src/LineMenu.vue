<template>
    <div class="left-menu">
        <div class="name-container" @click="emitsChangeDisplay">{{ menu.nom }} </div>
        <div class="options-container">
            <i class="bi bi-trash toright" @click="emitsDelete"></i>     
            <i class="bi bi-gear toright" @click="emitsModify"></i>
        </div>       
    </div>    
    <div class="menu-detail-container" v-show="menu.toShow">
        <p class="menu-elem" @click="emitsShowEntree">{{ menu.entree.nom }}</p>
        <p class="recette-left" v-show="menu.entree.toShow">{{ menu.entree.recette }}</p>

        <p class="menu-elem" @click="emitsShowPlat">{{ menu.plat.nom }}</p>
        <p class="recette-left" v-show="menu.plat.toShow">{{ menu.plat.recette }}</p>

        <p class="menu-elem" @click="emitsShowDessert">{{ menu.dessert.nom }}</p>
        <p class="recette-left" v-show="menu.dessert.toShow">{{ menu.dessert.recette }}</p>
    </div>
</template>

<script setup>

    defineProps({
        menu: {
            id: String,
            toShow: Boolean,
            nom: String,
            entree: String,
            plat: String, 
            dessert: String
        }
    })

    const emits = defineEmits(['changeDisplay', 'delete', 'modify', 'showEntree', 'showPlat', 'showDessert'])

    const emitsChangeDisplay = () => {
            emits('changeDisplay');
    }

    const emitsDelete = () => {
        emits('delete');
    }

    const emitsModify = () => {
        emits('modify');
    }

    const emitsShowEntree = () => {
        emits('showEntree');
    }

    const emitsShowPlat = () => {
        emits('showPlat');
    }

    const emitsShowDessert = () => {
        emits('showDessert');
    }

</script>

<style>

.left-menu {
    display:grid;
    grid-template-columns: 90% 1fr;
    border: solid rgb(253, 253, 253);
    border-radius: 5px;
    padding-left: 1rem;
    cursor: pointer;
    margin: 1px;
    margin-bottom: 5px;
    padding-bottom: 5px;
    
}

.left-menu:hover {
    background: rgb(140, 93, 136);
    color:white;
}

ul {
    list-style: none;
    padding-left: 5px !important;
}

.menu-detail-container {
    padding-left: 30px;
}

.menu-elem {
    border: solid rgb(248, 185, 219);
    margin-bottom: 0 !important;
    cursor: pointer;   
    border-radius: 5px;
}

.menu-elem:hover {
    background: rgb(248, 185, 219);
    color: white;
}

.recette-left  {
    background-color: rgb(255, 222, 252);
    padding-left: 5px;
    margin-bottom: 0 !important;
}

</style>