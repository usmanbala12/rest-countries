<script>
import axios from 'axios';
import { onMount } from 'svelte';
import CountryItem from "./CountryItem.svelte";

let countryList = [];

const getCountriesByRegion = async (region) => {
    const res = await axios.get(`https://restcountries.com/v3.1/region/${region}`)
    console.log(countryList)
    countryList = [...res.data]
    countryList = countryList 
    console.log(countryList)
}

const searchCountry = async (name) => {
    const res = await axios.get(`https://restcountries.com/v3.1/name/${name}`)
    countryList = res.data
    console.log(countryList)
}

onMount(
    async () => {
        const res = await axios.get('https://restcountries.com/v3.1/all')
        countryList = res.data
    }
)
</script>

<div>
    <div class="search-filter">
        <input type="text" class='search-input' placeholder="search for a country" on:change={(e) => searchCountry(e.target.value)}>
        <select name='region-filter' on:change={(e) => getCountriesByRegion(e.target.value)}>
            <option value="filter by region">filter by region</option>
            <option value="Africa">Africa</option>
            <option value="Americas">Americas</option>
            <option value="Asia">Asia</option>
            <option value="Europe">Europe</option>
            <option value="Oceania">Oceania</option>
            <!-- {optionValues} -->
        </select>
    </div>
    <div class="country-elements">
        {#each countryList as country (country.name.common)}
            <CountryItem {country} /> 
        {/each}
    </div>
</div>


<style>
    .search-filter {
        padding-inline: 2.5em;
        margin-block: 2.5em;
        display: flex;
        justify-content: space-between;
    }

    .search-filter input {
        width: 30%;
        background-color: hsl(var(--elements-color));
        color: hsl(var(--text-color));
        border: none;
        padding: 1em;
    }

    .search-filter select {
        border: none;
        background-color: hsl(var(--elements-color));
        color: hsla(var(--text-color) /  0.5);
        border-radius: 2px;
        padding-inline: 1em;
    }
    .country-elements {
        width: 90%;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
        row-gap: 2em;
        padding-inline: 1em;
    }

    @media (max-width: 375px) {
        .search-filter {
            flex-direction: column;
        }
        .search-filter input {
            width: 100%;
            margin-bottom: 1.5em;
        }
        .search-filter select {
            padding: 1em;
            width: 60%;
            font-size: 0.8rem;
        }
    }
</style>

