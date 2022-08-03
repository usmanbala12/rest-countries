<script>
import {Router, Route } from 'svelte-navigator'    
import Country from './components/Country.svelte';
import CountryList from "./components/CountryList.svelte";
import Layout from './components/Layout.svelte';
</script>


<Router>
    <Layout>
        <Route path='/' primary={false}>
            <CountryList />
        </Route>
        <Route path='/countries/:country' primary={false}>
            <Country />
        </Route>
    </Layout> 
</Router>


