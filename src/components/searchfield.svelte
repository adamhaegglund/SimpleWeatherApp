<script lang=ts >

    import {selectedCity} from './stores';
    import { onMount } from 'svelte';

    onMount(() => {
    document.addEventListener('click', handleClickOutside);
    return () => {
      document.removeEventListener('click', handleClickOutside);
    };
  });
  function handleClickOutside(event: any) {
    if (!event.target.closest('.dropdown')) {
      cities = [];
    }
  }

    let city: any;

    selectedCity.subscribe(value => {
        city = value;
    })

    

    let cities: any = [];
    let inputValue = "";
    const API_URL = "https://weatherapi-com.p.rapidapi.com/search.json";
    const API_KEY = "1111347a62mshb686412459936abp12afbcjsn960472af610b";
  
    async function getCities(query: any) {
      if (inputValue.trim() == "") {
      } else {
        const response = await fetch(`${API_URL}?q=${query}`, {
          "method": "GET",
          "headers": {
            "x-rapidapi-host": "weatherapi-com.p.rapidapi.com",
            "x-rapidapi-key": API_KEY
          } 
        });
        const data = await response.json();
        cities = data.map((item:any) => ({ name: item.name, country: item.country }));
        
      }
    }
    
    function selectCity(city: any) {
    selectedCity.set(city);
    }

    function emptyCityArray(){
      cities.length = 0;
    }

    function handleCityClick(cityName: any) {
    inputValue = '';
    selectCity(cityName);
    emptyCityArray();
  }

  </script>

  <div class="container">
    <h1>FIND THE WEATHER OF YOUR CURRENT LOCATION</h1>
  
    <div class="searchfield">
      <input type="text" placeholder="Enter a city" bind:value={inputValue} on:input={() => getCities(inputValue)} />
      
      {#if cities.length > 0}
        <div class="dropdown">
          <ul>
            {#each cities as city}
              <li on:click={() => handleCityClick(city.name)} 
                  on:keydown={() => selectCity(city.name)}>
                  {city.name}, {city.country}
              </li>
            {/each}
          </ul>
        </div>
      {/if}
    </div>
  </div>


  <style>
    
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }

    .dropdown {
    position: absolute;
    background-color: #ffffff;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    z-index: 1;
  }

  .dropdown ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  .dropdown ul li {
    padding: 12px 16px;
    cursor: pointer;
  }

  .dropdown ul li:hover {
    background-color: #ddd;
  }

  input{
    padding: 10px;
    border-radius: 5px;
    border: 1px solid #ccc;
    width: 100%;
  }

  input:focus {
  outline: none;

}
  </style>
