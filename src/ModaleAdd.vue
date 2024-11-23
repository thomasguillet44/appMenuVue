<template>
    <div class="bloc-modale" v-show="visible">
        <div class="overlay" @click="emitsClose"></div>
        <div class="modale card">
            <div class="btn-modale btn btn-danger" @click="emitsClose">X</div>
            <input class="mt-2" type="text" placeholder="Nom du menu" v-model="nouveauMenu.nom">
            <input class="mt-2" type="text" placeholder="Entree" v-model="nouveauMenu.entree">
            <input class="mt-2" type="text" placeholder="Plat" v-model="nouveauMenu.plat">
            <input class="mt-2" type="text" placeholder="Dessert" v-model="nouveauMenu.dessert">
            <div class="btn btn-success mt-2" @click="emitsAdd">Valider l'ajout</div>
        </div>
    </div>
</template>

<script setup>

    import {ref} from 'vue';

    defineProps({
        visible: Boolean
    });

    const nouveauMenu = ref({
        nom:'', 
        entree:'', 
        plat:'',
        dessert:''
    });

    const emits = defineEmits(['close', 'addMenu']);

    const emitsClose = () => {
        emits('close');
    }

    const emitsAdd = () => {
        emits('addMenu', {nouveauMenuToSend : nouveauMenu.value});
        resetElement();
        emitsClose();
    }

    function resetElement() {
        nouveauMenu.value = {
            nom:'', 
            entree:'', 
            plat:'',
            dessert:''
        }
    }

</script>

<style scoped>
.bloc-modale {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.overlay {
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}

.modale {
  background: #f1f1f1;
  color: #333;
  padding: 50px;
  position: fixed;
  top: 30%;
}

.btn-modale {
  position: absolute;
  top: 10px;
  right: 10px;
}
</style>