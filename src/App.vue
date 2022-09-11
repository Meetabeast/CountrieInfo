<template>
  <div>
    <my-theme></my-theme>
    <div class="header">
      <h1>Countries</h1>
      <input type="text" id="searchCountrie" class="searchCountrie" placeholder="Search Countrie">
    </div>

    <div class="container">
      <div class="countries">
        <div class="countrie" v-for="countrie in countries" :key=countrie>
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

      <div class="footer">
        <div class="footer-container">
          <a href="https://github.com/Meetabeast/CountrieInfo" target="_blank">
            <p>CountrieInfo only show's a demo<br>Show the Code on Github</p>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import myTheme from './components/Theme.vue';

export default {
  name: 'App',
  components: {
    myTheme
  },
  data() {
    return {
      countries: []
    }
  },
  mounted() {
    axios.get('https://restcountries.com/v3.1/all').then(res => {
      for(var i = 0; i < res.data.length; i++) {
        let array = {
          flag: res.data[i].flags.png,
          languages: res.data[i].languages,
          region: res.data[i].region,
          population: res.data[i].population,
          name: res.data[i].name.common,
          maps: res.data[i].maps.googleMaps,
        };
        this.countries.push(array);
      }
    });

    let input = document.getElementById("searchCountrie");

    input.onkeyup = function() {
      let searchInput = document.getElementById("searchCountrie").value;
      searchInput = searchInput.toLowerCase();
      let allCountries = document.getElementsByClassName('countrie-name');
      let allCountriesCard = document.getElementsByClassName('countrie');

      for(var i = 0; i < allCountries.length; i++) {
        if(!allCountries[i].innerHTML.toLowerCase().includes(searchInput)) {
          allCountriesCard[i].style.display = "none";
        } else {
          allCountriesCard[i].style.display = "block"
        }
      }
    }
  }
}
</script>

<style>
body {
  background-color: var(--background1);
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.header {
  justify-content: center;
  text-align: center;
  color: rgb(255, 255, 255);
  font-family: Arial, sans-serif;
}

.searchCountrie {
  display: block;
  background-color: rgb(21, 23, 24);
  margin-right: auto;
  margin-left: auto;
  border: none;
  color: rgb(255, 255, 255);
  font-size: 1rem;
  padding: 1rem;
  margin-bottom: 2rem;
  border-radius: 10px;
  width: 300px;
}

.countrie {
  padding: 8px 8px;
  margin: 22px;
  height: 450px;
  width: 300px;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  float: left;
  position: relative;
  overflow: hidden;
  background-color: var(--cardColor);
}

.countrie .informations {
  color: var(--textColor);
  font-family: Arial, sans-serif;
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
}

.footer {
  padding-top: 10vh;
  width: 100%;
  font-family: Arial, sans-serif;
  font-size: 19px;
}

.footer-container a {
  text-decoration: none;
  color: var(--textColor);
  justify-content: center;
  align-items: center;
  text-align: center;
}

::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  background: rgb(23, 27, 31);
}

::-webkit-scrollbar-thumb {
  background:#007bff;
  border-radius: 10px;
}

@media(max-width: 700px) {
  .countrie {
    margin-left: 30px;
  }
}

</style>
