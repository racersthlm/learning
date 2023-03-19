
<script lang=ts>
    import { onMount } from "svelte";
    let promise: Promise<any>;
    onMount(async () => {
    const response =  await fetch("https://swapi.dev/api/people/?format=json");
    promise = response.json();
    });


function  getPlanetData(url)
{
    return "Tatoine";
}

</script>


{#await promise}
<h2>Waiting...</h2>
    
{:then results} 

{#if results != undefined}
<h1>Starwars Characters</h1>
<table>
   
<tr>
    <th>Name</th>
    <th>Height</th>
    <th>Mass</th>
    <th>Hair Color</th>
    <th>Skin Color</th>
    <th>Eye Color</th>
    <th>Birth Year</th>
    <th>Gender</th>
    <th>Homeworld</th>
    <th>id</th>
</tr>
{#each results.results as character}
<tr>
    <td>{character.name}</td>
    <td>{character.height}</td>
    <td>{character.mass}</td>
    <td>{character.hair_color}</td>
    <td>{character.skin_color}</td>
    <td>{character.eye_color}</td>
    <td>{character.birth_year}</td>
    <td>{character.gender}</td>
    <td>{getPlanetData(character.homeworld)}</td>
    
</tr>
{/each}
</table>
{/if}
{:catch error}
<h4>Something went wrong: {error}</h4>
{/await}

