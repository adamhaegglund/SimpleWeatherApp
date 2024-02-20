<script lang="ts">

    import {selectedCity} from './stores';

    let city: any;

    selectedCity.subscribe(value => {
        city = value;
    })

    function setCity(city: any) {
    selectedCity.set(city);
    }
</script>

<button on:click={() => setCity(null)}>Back to search</button>

<style>
    button {
        margin-top: 20px;
        padding: 10px;
        background-color: #ffffff;
        border: 1px solid black;
        border-radius: 3px;
        cursor: pointer;
    }
</style>