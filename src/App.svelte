<script>
	import Pokeimage from "./Pokeimage.svelte"
	let searchname;
	let details;
	let pokelistpromise = catchpokemon("https://pokeapi.co/api/v2/pokemon/?offset=0&limit=898");
	async function catchpokemon(api_link){
		const res = await fetch(api_link);
		const data = await res.json();

		if(res.ok){
			
			return(data);
		}
		else{
			throw new Error(data);
		}
		
	}

</script>

<main>
	<p>type in your pokemons name</p>
	<input bind:value={searchname}>
	<button on:click={() => (catchpokemon())}></button>

	{#await pokelistpromise}
		<p>... loading</p>
	{:then pokelist}
		{#each pokelist.results as pokemon}
		{#if pokemon.name == searchname}
		<p>{pokemon.name}</p>
		<Pokeimage link="{pokemon.url}"></Pokeimage>
		
		{/if}
		{/each}
	{:catch error}
		<p>error</p>
	{/await}
	


</main>

