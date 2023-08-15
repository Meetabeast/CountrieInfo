<script setup>
import myTheme from "./components/myTheme.vue";
import { onMounted, ref } from 'vue';
const countries = ref([]);


  onMounted(() => {
    fetch("https://restcountries.com/v3.1/all").then(res => res.json().then(data => {
      for (var i = 0; i  < data.length; i++) {
        const array = {
          flag: data[i].flags.png,
          languages: data[i].languages,
          region: data[i].region,
          population: data[i].population,
          name: data[i].name.common,
          maps: data[i].maps.googleMaps,
        };

        countries.value.push(array);
      }
    }));
  });
</script>

<template>
    <div class="wrapper">
      <myTheme></myTheme>
      <div class="header">
        <h1>Countries</h1>
        <input type="text" id="searchCountrie" class="searchCountrie" placeholder="Search Countrie">
      </div>
      <div class="container">
        <div class="countrie {{ countrie.name }}" v-for="countrie in countries" :key="countrie">
          <img :src=countrie.flag alt="Countrie Image" class="countrie-image">
          <div class="informations">
            <p>
              Name: <span class="countrie-name">{{countrie.name}}</span>
            </p>
            <p>
              Region: <span class="name">{{countrie.region}}</span>
            </p>
            <p>
              Population: <span class="name">{{countrie.population.toLocaleString()}}</span>
            </p>  
            <p>
            
            </p>  
          </div>
          <a :href=countrie.maps class="maps" target="_blank">Maps</a>
        </div>
      </div>
    </div>
</template>

<style>
* {
  padding: 0;
  margin: 0;
}

body {
  background-color: #0d1117;
  color: #FFF;
  font-family: Arial, sans-serif;
  transition: background-color 2.5s;
}

.header {
  padding-top: 2rem;
  justify-content: center;
  text-align: center;
  color: rgb(255, 255, 255);
  font-family: Arial, sans-serif;
}

.searchCountrie {
  display: block;
  background-color: #24292e;
  margin-right: auto;
  margin-left: auto;
  border: none;
  color: rgb(255, 255, 255);
  font-size: 1rem;
  padding: 1rem;
  margin-top: 2rem;
  margin-bottom: 2rem;
  border-radius: 10px;
  width: 500px;
  transition: background-color 2.7s, color 2.7s;
}

.searchCountrie:focus {
  outline: none;
  transform: scale(1.05);
  transition: 1.5s ease-out;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
}

.countrie {
  padding: 8px 8px;
  margin: 22px;
  margin-right: 40px;
  height: 350px;
  width: 300px;
  border-radius: 8px;
  background-color: #24292e;
  overflow: hidden;
  transition: background-color 2.8s;
}

.countrie .informations {
  line-height: 2.5;
  color: #FFF;
}

.countrie-image {
  width: 100%;
  height: 150px;
  border-radius: 15px;
}

.maps {
  display: inline-block;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.35rem;
  transition: color .15s ease-in-out, background-color .15s ease-in-out, border-color .15s ease-in-out, box-shadow .15s ease-in-out;
  color: rgb(255, 255, 255);
  background-color: #007bff;
  text-decoration: none;
  font-family: Arial, sans-serif;
}

.countrie:hover {
  transform: scale(1.05);
  transition: 1.5s;
  box-shadow: 0 0 20px #24292e;
}

::-webkit-scrollbar {
  width: 10px;
}


::-webkit-scrollbar-thumb {
  background:#007bff;
  border-radius: 10px;
}

@media screen and (max-width: 768px) {
  .searchCountrie {
    width: 200px;
  }

  .countrie {
    margin-right: 20px;
  }
}
</style>
