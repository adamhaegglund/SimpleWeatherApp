<script lang=ts>
    
    import {selectedCity} from './stores';
    
    let city: any;

    selectedCity.subscribe(value => {
        city = value;
    })

    $: getData(city), selectedCity;
    const options = {
        method: 'GET',
        headers: {
            'X-RapidAPI-Key': '1111347a62mshb686412459936abp12afbcjsn960472af610b',
            'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
        }
    };
    
    let weatherData: any;
    let weatherDataLocation: any;
    async function getData(city: any){
        const response = await fetch('https://weatherapi-com.p.rapidapi.com/current.json?q='+city, options);
        const data = await response.json();
        weatherData = data.current;
        weatherDataLocation = data.location;
    };
    
    getData(city);

    </script>
    
    {#if city != null}
        {#if weatherData}
        <div class="weather-info">
            <h2>Weather in {weatherDataLocation.name}, {weatherDataLocation.country}</h2>
            <p class="weather-detail"><span>Temperature:</span> <span>{weatherData.temp_c}°C</span></p>
            <p class="weather-detail"><span>Wind:</span> <span>{weatherData.wind_kph} km/h</span></p>
            <p class="weather-detail"><span>Feels like:</span> <span>{weatherData.feelslike_c}°C</span></p>
            <p class="weather-detail"><span>Humidity:</span> <span>{weatherData.humidity}%</span></p>
            <p class="weather-detail"><span>Condition:</span> <span>{weatherData.condition.text}</span></p>
          </div>
        {/if}
    {/if}
        

    <style>
        .weather-detail {
          display: flex;
          justify-content: space-between;
        }
      </style>