<script setup>
//defineProps(["title",'id', 'body'])

defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: "Sin descripción",
  },
  cambiarFavoritoNombre: Function,
});
/* const emit = defineEmits(["cambiarFavoritoNombre"]); */

//emit emit('cambiarFavorito', title)"
</script>

<template>
  <div class="card">
    <h5>{{ id }} - {{ title }}</h5>

    <p>{{ body }}</p>

    <button
      @click="cambiarFavoritoNombre(title)"
      class="btn btn-outline-primary"
    >
      Favorito
    </button>
  </div>
</template>
