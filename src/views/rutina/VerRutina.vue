<script setup>
import { ref, onMounted, defineProps, computed } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";
import BotonRojo from "@/components/BotonRojo.vue";
import BotonGris from "@/components/BotonGris.vue";

const props = defineProps({
  id: String,
  rutina: Object,
});

const route = useRoute();

const rutina = ref({
  ejercicios: [],
});

const cargarDetalleRutina = () => {
  axios
    .get(`http://localhost:3000/rutinas/${props.id}`)
    .then((response) => {
      rutina.value = response.data;
    })
    .catch((error) => {
      console.error(error);
    });
};

const returnLink = computed(() => {
  return route.query.from || "/Rutinas";
});

onMounted(() => {
  cargarDetalleRutina();
  console.log("rutina ID:", props.id);
});
</script>

<template>
  <main>
    <div class="volver">
      <BotonRojo :link="returnLink" />
    </div>
    <div class="info-rutina">
      <h2 style="text-align: center">{{ rutina.nombre }}</h2>
      <table>
        <thead>
          <tr>
            <th>Ejercicio</th>
            <th>Peso</th>
            <th>Repeticiones</th>
            <th>Series</th>
            <th>Descanso</th>
            <th>Detalles</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="ejercicio in rutina.ejercicios" :key="ejercicio.id">
            <td>{{ ejercicio.nombre }}</td>
            <td>{{ ejercicio.pesoRecomendado }}</td>
            <td>{{ ejercicio.repeticiones }}</td>
            <td>{{ ejercicio.series }}</td>
            <td>{{ ejercicio.descanso }}</td>
            <td>
              <BotonGris
                :link="`/DetalleEjercicio/${ejercicio.id}`"
                button-text="Detalles"
              />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>
<style scoped>
main {
  padding: min(30px, 7%);
  background-color: #0f1017;
  display: grid;
  grid-template-rows: auto 1fr;
  grid-template-areas:
    "navbar"
    "main";
}

h2 {
  color: white;
  margin: 0;
  padding: 10px 0; /* Adjust this padding as necessary */
  text-align: center;
}

.info-rutina {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 20px; /* Reduce the margin-top to decrease the spacing */
}

.info-rutina table {
  border-radius: 10px;
  width: 50%;
  margin: 10px 0; /* Add some margin to create space between the heading and the table */
  height: auto;
}

.info-rutina th {
  background-color: #ad283d;
  color: white;
  padding: 10px;
  text-align: left;
  border: none;
}

.info-rutina td {
  padding: 10px;
  background-color: white;
  border: none;
  color: #000;
  text-align: left;
}
</style>
