<template>
    <div class="left-menu">
        <div class="name-container" @click="emitsChangeDisplay">{{ menu.nom }} </div>
        <div class="options-container">
            <i class="bi bi-trash toright" @click="emitsDelete"></i>     
            <i class="bi bi-gear toright" @click="emitsModify"></i>
        </div>       
    </div>    
    <div class="menu-detail-container" v-show="menu.toShow">
        <div class="menu-elem" @click="emitsShowEntree">
            <i v-show="!menu.entree.toShow" class="bi bi-caret-right"></i> 
            <i v-show="menu.entree.toShow" class="bi bi-caret-down"></i>
            <span>{{ menu.entree.nom }}</span>           
        </div>  
        <p class="recette-left" v-show="menu.entree.toShow">{{ menu.entree.recette }}</p>

        <div class="menu-elem" @click="emitsShowPlat">
            <i v-show="!menu.plat.toShow" class="bi bi-caret-right"></i> 
            <i v-show="menu.plat.toShow" class="bi bi-caret-down"></i>
            <span>{{ menu.plat.nom }}</span>            
        </div>
        <p class="recette-left" v-show="menu.plat.toShow">{{ menu.plat.recette }}</p>
       
        <div  class="menu-elem" @click="emitsShowDessert">
            <i v-show="!menu.dessert.toShow" class="bi bi-caret-right"></i> 
            <i v-show="menu.dessert.toShow" class="bi bi-caret-down"></i>
            <span>{{ menu.dessert.nom }}</span>
        </div>
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
    border-radius: 5px;
    padding-left: 1rem;
    cursor: pointer;
    padding-bottom: 5px;
    border: solid black;   
}

.left-menu:hover {
    background: gray;
    border: solid gray;
    color:white;
}

ul {
    list-style: none;
    padding-left: 5px !important;
}

.menu-elem {
    margin-bottom: 0 !important;
    cursor: pointer;
}

.menu-elem:hover {
    background: rgb(70, 187, 74);
    color: white;
}

.menu-detail-container {
    margin-left: 3px;
}

.recette-left  {
    border: solid rgb(36, 202, 30);
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    padding-left: 3px;
    margin-bottom: 0 !important;
}

</style>