<script>
import { useParams, useNavigate } from 'svelte-navigator';
import { onMount } from 'svelte';
import axios from 'axios';

    const params = useParams()
    const navigate = useNavigate()
    let country

    onMount(async () => {
        const res = await axios.get(`https://restcountries.com/v3.1/name/${$params.country}?fullText=true`);
        country = res.data[0]
    })

    const backToHome = () => {
        navigate('/')
    }
</script>

{#if country}
<div class="country">
    <button on:click={backToHome}>back</button>
    <div class="details">
        <img src={country.flags.png} alt='country flag'>
        <div class="details-text">
            <h2>{country.name.common}</h2>
            <div class="inner-details">
                <div class="main">
                    <p>Native Name: <span class="val">{country.name.common}</span></p>
                    <p>Population: <span class="val">{country.population.toLocaleString()}</span></p>
                    <p>Region: <span class="val">{country.region}</span></p>
                    <p>Sub Region: <span class="val">{country.subregion}</span></p>
                    <p>Capital: <span class="val">{country.capital}</span></p>
                </div>
                <div class="aux">
                    <p>Top Level Domain: <span class="val"></span>{country.tld}</p>
                    <p>Currencies: {#each Object.keys(country.currencies) as currency (currency)} 
                            <span class="val">{currency}</span>
                        {/each}
                    </p>
                    <p>Languages:{#each Object.values(country.languages) as language (language)} 
                        <span class="val">{language}</span>
                    {/each}
                    </p>
                </div>   
            </div>
            <div class="border-countries">
                Border countries: {#each country.borders as borders (borders)}
                    <button>{borders}</button>
                {/each}
            </div>
        </div>
    </div>
</div> 
{/if}

<style>
    .country {
        display: flex;
        flex-direction: column;
        width: 85%;
        margin: 0 auto;
        height: 100vh;
    }
    
    .country > button {
        margin-block: 2em;
        width: 10%;
        background-color: hsl(var(--elements-color));
        border: none;
        padding-block: 0.5em;
        color: inherit;
        border-radius: 3px;
        box-shadow: 5px 5px 5px 5px hsla(0, 0, 0, 0.8);
    }
    .details {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .details img {
        width: 45%;
        height: 100%;
    }

    .details-text {
        width: 50%;
    }

    .inner-details {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        margin-block: 2em;
    }

    .border-countries > button {
        width: auto;
        margin-inline: 0.5em;
        background-color: hsl(var(--elements-color));
        border: none;
        padding: 0.3em;
        color: black;
        border-radius: 3px;
        box-shadow: 5px 5px 5px 5px hsla(0, 0, 0, 0.8);
    }
    .country > button:hover {
        cursor: pointer;
    }

    @media (max-width: 430px) {
        .country > button {
            width: 30%
        }

        .details {
            flex-direction: column;
            align-items: flex-start;
            justify-content: flex-start;
        }

        .inner-details {
            flex-direction: column;
            align-items: flex-start;
        }

        .details-text {
            width: 100%;
        }
        .details-text h2 {
            margin-block: 1em;
        }
        .aux {
            margin-top: 1.5em;
        }
        .details img {
        width: 100%;
        height: 100%;
        }
        .border-countries {
            padding-bottom: 2em;
        }

    }

</style>


