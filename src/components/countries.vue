<template>
    <div>
        <div class="container">
            <div class="countries-card" v-for="countrie in countries" :key=countrie>
                <p>{{countrie.common}}</p>
                <img :src="countrie" class="countrie-img">
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "myCountries",
    data() {
        return {
            countries: []
        }
    },
    async mounted() {
        this.url = 'https://restcountries.com/v3.1/all';
        let resp = await axios.get(this.url);

        resp.data.map(c => {
            let Infos = {
                name: c.data.name || "No Name",
                maps: c.data.maps.googleMaps,
                flag: c.data.flags.png,
                region: c.data.region,
                population: c.data.population
            };
            console.log(Infos)
        })
    }
}
</script>

<style>
    .container {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }

    .countries-card {
        padding: 8px;
        margin: 12px;
        height: 250px;
        width: 300px;
        border-radius: 8px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-direction: column;
        float: left;
        position: relative;
    }
</style>