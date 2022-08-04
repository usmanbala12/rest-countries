<script>
    import { Link } from 'svelte-navigator';
    export let country;

</script>

<div class="country-card">
    <div class="coutry-flag">
        <Link to={`countries/${country.name.common}`}>
        <img src={country.flags.png} alt='country flag'>
        </Link>
    </div>
    <div class="country-details">
        <h3>{country.name.common}</h3>
        <p>Population: <span class="val">{country.population.toLocaleString()}</span></p>
        <p>Region: <span class="val">{country.region}</span></p>
        <p>Capital: <span class="val">{country.capital}</span></p>
    </div>
</div>

<style>
    .country-card {
        background-color: hsl(var(--elements-color));
        width: 22%;
        display: flex;
        flex-direction: column;
        flex-wrap: nowrap;
    }
    .country-card img {
        width: 100%;
    }
    .country-details {
        padding: 10px;
        display: flex;
        flex-direction: column;
    }

    .country-details h3 {
        padding-block: 1em;
    }

    @media (max-width: 375px) {
	.country-card {
		width: 100%;
        border-radius: 10px;
	}
}
</style>