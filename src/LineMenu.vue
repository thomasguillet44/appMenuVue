<template>
    {{ menu.nom }} <button @click="emitsDelete">Supprimer menu</button> <button @click="emitsChangeDisplay">{{ menu.toShow ?'Cacher menu' : 'Afficher menu' }}</button>
    <div v-show="menu.toShow">
        <p>{{ menu.entree }}</p>
        <p>{{ menu.plat }}</p>
        <p>{{ menu.dessert }}</p>
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

    const emits = defineEmits(['changeDisplay', 'delete'])

    const emitsChangeDisplay = () => {
            emits('changeDisplay');
    }

    const emitsDelete = () => {
        emits('delete');
    }

</script>