<script setup>
import BotonRojo from '@/components/BotonRojo.vue';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const peso = ref(null);
const altura = ref(null);
const sexo = ref(null);
const dias = ref(null);
const error = ref("");
const router = useRouter();

const enviarDatos = () => {
    error.value = "";
    localStorage.setItem('peso', peso.value);
    localStorage.setItem('altura', altura.value);
    localStorage.setItem('sexo', sexo.value);
    localStorage.setItem('dias', dias.value);
    router.push('/CoachObjetivo'); 
};

</script>

<template>

    <main class="coach-container">
        <div class="grid-container">
            <div class="boton">
                <BotonRojo link="/" button-text="Volver" />
            </div>
            <div class="mensaje-inicial">
                <h2>COACH VIRTUAL</h2>
                <p>Antes de comenzar, necesitamos conocerte...</p>
            </div>
        </div>
        <div class="coach-virtual">
            <div class="options">
                <form @submit="enviarDatos">
                    <div class="options">

                        <!-- Altura -->
                        <div class="option">
                            <label for="altura">¿Cuánto mides?</label>
                            <img src="../coach/img-coach/limite-de-altura.png" alt="altura.png">
                            <input type="number" id="altura" placeholder="Cm" required v-model="altura" min="120"
                                max="250">
                        </div>

                        <!-- Peso -->
                        <div class="option">
                            <label for="peso">¿Cuánto pesas?</label>
                            <img src="../coach/img-coach/bascula(1).png" alt="bascula.png">
                            <input type="number" id="peso" placeholder="Kg" required v-model="peso" min="20" max="560">
                        </div>

                        <!-- Sexo -->
                        <div class="option">
                            <label>¿Cuál es tu sexo?</label>
                            <img src="../coach/img-coach/masculino-y-femenino.png" alt="sexos.png">
                            <div class="sexo-options">
                                <input type="radio" id="masculino" name="sexo" value="masculino" v-model="sexo"
                                    required>
                                <label for="masculino">Masculino</label>
                                <input type="radio" id="femenino" name="sexo" value="femenino" v-model="sexo" required>
                                <label for="femenino">Femenino</label>
                            </div>
                        </div>

                        <!-- Días Disponibles de la Semana -->
                        <div class="option">
                            <label for="dias">¿Cuántos días entrenarás?</label>
                            <img src="../coach/img-coach/calendario.png" alt="calendario.png">
                            <input type="number" id="dias" placeholder="1 a 7" required v-model="dias" min="1" max="7">
                        </div>
                    </div>

                    <!-- Mostrar error si existe -->
                    <div v-if="error" class="error-message">
                        <p>{{ error }}</p>
                    </div>

                    <button type="submit" class="boton-continuar">Continuar</button>
                </form>
            </div>
        </div>

    </main>

</template>

<style scoped>
.coach-container {
    font-family: 'Poppins', sans-serif;
    background-color: #292828;
    color: #fff;
}

.grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}

.mensaje-inicial {
    text-align: center;

    h2 {
        font-size: 2em;
        margin-bottom: 10px;
        margin-top: 20px;
    }
}

.boton {
    margin-left: 30px;
}

.coach-virtual {
    text-align: center;
    padding: 20px;
    margin: 8px auto;
    width: 90%;
    max-width: 1200px;
    background-color: #212121;
    color: white;
    border-radius: 10px;
}

.coach-virtual h2 {
    font-size: 2em;
    margin-bottom: 10px;
}

.coach-virtual p {
    margin-bottom: 30px;
    font-size: 1.2em;
}

/* Estilos para las opciones (peso, sexo, altura) */
.options {
    display: flex;
    justify-content: space-between;
    gap: 40px;
}

.option {
    background-color: #2c2c2c;
    padding: 20px;
    border-radius: 10px;
    width: 30%;
    text-align: center;
}

.option img {
    height: 200px;
    margin-bottom: 10px;
}

.option label {
    display: block;
    margin-bottom: 10px;
    font-size: 1em;
}

.option input[type="number"] {
    width: 70%;
    padding: 10px;
    border-radius: 5px;
    border: none;
    font-size: 1em;
    margin-top: 10px;
    background-color: #3c3c3c;
    color: white;
}

/* Estilo para las opciones de sexo */
.sexo-options {
    display: inline-flex;
    align-content: center;
    justify-content: space-around;
}

.sexo-options input[type="radio"] {
    margin: 20px 5px 0 0;
}

.sexo-options label {
    font-size: 1em;
    margin: 20px 10px 0 5px
}

.boton-continuar{
    background-color: #d22;
    color: white;
    border: none;
    padding: 15px 30px;
    font-size: 1.2em;
    border-radius: 10px;
    cursor: pointer;
    margin-top: 30px;
}

.boton-continuar:hover{
    background-color: #c00;
}
</style>