<script>
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";

const route = useRoute();
const router = useRouter();

const nombre = ref("");
const descripcion = ref("");
const nivelDificultad = ref("");
const grupoMuscular = ref("");
const ejerciciosDisponibles = ref([]);
const ejercicios = ref([]);

const cargarEjercicios = async () => {
  try {
    const res = await fetch("http://localhost:3000/ejercicios");
    ejerciciosDisponibles.value = await res.json();
  } catch (error) {
    console.error("Error al obtener los ejercicios:", error);
  }
};

const editarRutina = async () => {
  const rutinaActualizada = {
    nombre: nombre.value,
    descripcion: descripcion.value,
    nivelDificultad: nivelDificultad.value,
    grupoMuscular: grupoMuscular.value,
    ejercicios: ejercicios.value,
  };

  try {
    await axios.put(
      `http://localhost:3000/rutinas/${route.params.id}`,
      rutinaActualizada
    );
    router.push("/AdminListaRutinas");
  } catch (error) {
    console.error("Error al editar la rutina:", error);
    alert("Error al editar la rutina");
  }
};

onMounted(() => {
  cargarEjercicios();
});
</script>

<template>
  <div class="container">
    <form @submit.prevent="editarRutina">
      <h2 class="form-header">Editar una Rutina</h2>
      <div class="form-row">
        <div class="left">
          <!-- Campos de texto -->
          <p>Nombre de la Rutina</p>
          <input type="text" v-model="nombre" placeholder="Nombre" required />
          <p>Descripción</p>
          <textarea
            v-model="descripción"
            placeholder="descripción"
            rows="2"
          ></textarea>
          <div class="valores-def">
            <!-- Peso recomendado y grupo muscular -->
            <p>Nivel de Dificultad</p>
            <div class="nivel">
              <select v-model="nivelDificultad" required>
                <option value="">Seleccionar categoría</option>
                <option value="principiante">principiante</option>
                <option value="intermedio">intermedio</option>
                <option value="avanzado">avanzado</option>
              </select>
            </div>
            <p>Grupo Muscular</p>
            <select v-model="grupoMuscular" required>
              <option value="">Seleccionar categoría</option>
              <option value="Tren Superior">Tren Superior</option>
              <option value="Core">Core</option>
              <option value="Tren Inferior">Tren Inferior</option>
            </select>
          </div>
          <p>Escojer Ejercicios</p>
          <select v-model="ejercicioSeleccionado">
            <option value="" disabled>Seleccionar ejercicio</option>
            <option
              v-for="ejercicio in ejerciciosDisponibles"
              :key="ejercicio.id"
              :value="ejercicio.nombre"
            >
              {{ ejercicio.nombre }}
            </option>
          </select>
          <button class="add-exercise" type="button" @click="agregarEjercicio">
            Añadir Ejercicio
          </button>
          <ul>
            <li v-for="(ejercicio, index) in ejercicios" :key="index">
              {{ ejercicio.nombre }}
            </li>
          </ul>
        </div>
      </div>

      <!-- Botones de acción -->
      <div class="buttons">
        <button
          type="button"
          @click="$router.push('/AdminListaRutinas')"
          class="cancel-button"
        >
          Cancelar
        </button>
        <button type="submit" class="save-button">Guardar</button>
      </div>
    </form>
  </div>
</template>

<style scoped>
.container {
  margin-left: 270px;
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0 60px;
  background-color: #0d0e16;
}

form {
  background-color: #ffffff;
  color: #000000;
  border-radius: 10px;
  padding: 2% 4%;
  width: 900px;
  height: auto;
  margin: auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-header {
  font-size: 24px;
  font-weight: bold;
  text-align: center;
}

.form-row {
  display: flex;
  justify-content: space-between;
  gap: 40px;
}

form input {
  flex: 1;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 100%;
  font-size: 16px;
}

form select {
  flex: 1;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 100%;
  font-size: 16px;
  background-color: #ffffff;
  color: #000000;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

textarea {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 16px;
  font-family: inherit;
  resize: vertical;
  height: 100px;
}

.valores-def {
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  gap: 10px;
}

.left {
  display: flex;
  flex-direction: column;
  gap: 15px;
  flex: 1;
}

.right {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-left: 15px;

  h3 {
    text-align: left;
  }
}

.buttons {
  display: flex;
  justify-content: space-between;
}

.cancel-button,
.save-button {
  padding: 10px;
  font-size: 18px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  width: 45%;
}

.save-button {
  background-color: #d32f2f;
  color: #fff;
}

.save-button:hover {
  background-color: #b71c1c;
}

.cancel-button {
  background-color: #e0e0e0;
  color: #000;
}

.cancel-button:hover {
  background-color: #bdbdbd;
}
</style>
