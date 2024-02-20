<script lang="ts">
    import Weather from '../components/weather.svelte'
    import Searchfield from '../components/searchfield.svelte';   
	import ResetCity from '../components/resetCity.svelte';

    import {selectedCity} from '../components/stores';
    
    let city: any;

    selectedCity.subscribe(value => {
        city = value;
    })
</script>

<main class="app">
    
        {#if city == null}
        <Searchfield/>
        {:else}
        <div class="city-container">
            <Weather/>
            <ResetCity/>
        </div>
        {/if}
   
</main>

<style>
    .app{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 90%;
    }

    .city-container{
        display: flex;
        flex-direction: column;
    }
    
    
</style>