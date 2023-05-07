<script setup>
    import {ref, onMounted} from 'vue'

    const API_KEY = '91b20457bea58abb4f885a2ea694e72f'
    const API_URL = `http://api.openweathermap.org/data/2.5/forecast?id=524901&appid=${API_KEY}`;

    const weatherData = ref(null)
    const error = ref(false)

    onMounted(async ()=>{
        try{
            console.log("Starting fetching data")
            const response = await fetch(API_URL);
            const data = await response.json();
            weatherData.value = data;
        }
        catch (error){
            console.log(error)
            error.value = true
        }
    })
</script>

<template>
    <div>
        <div v-if="error">
            <p>Error consiguiendo datos</p>
        </div>
        <div v-else-if="weatherData">
            <h2>{{ weatherData.name }}</h2>
            <p>Temperatura: {{ weatherData.main.temp }}ºC</p>
            <p>Descripción: {{ weatherData.weather[0].description }}</p>
        </div>
        <div v-else>
            <p>Cargando...</p>
        </div>
    </div>
    
</template>

<style>
</style>