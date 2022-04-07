<script>
    export let link;
    let pokemonpromise = current_pokemon(link);
    async function current_pokemon(api_link){
		const res = await fetch(api_link);
		const pokemon_data = await res.json();
		

		if(res.ok){
			
			return(pokemon_data);
		}
		else{
			throw new Error(pokemon_data);
		}
		
	}
</script>



{#await pokemonpromise }
    ..loading
{:then pokemondetails} 
<img src="{pokemondetails.sprites.front_default}" alt="error">
<img src="{pokemondetails.sprites.front_shiny}" alt="error">

{/await}
