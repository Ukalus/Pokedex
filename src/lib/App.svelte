<script>
	import Pokeimage from "./Pokeimage.svelte"
	let searchname;
	let pokelistpromise = catchpokemon("https://pokeapi.co/api/v2/pokemon/?offset=0&limit=151");
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
	<div class="centerpokedex pokedex">
		<h1 class="container">Pokedex</h1>
		<input class="container searchbar" bind:value={searchname} placeholder="Type in your pokemon">
		{#await pokelistpromise}
			<p>... loading</p>
		{:then pokelist}
			{#each pokelist.results as pokemon}
				{#if pokemon.name.includes(searchname)}
				<Pokeimage link="{pokemon.url}"></Pokeimage>
				{/if}
			{/each}
		{:catch error}
			<p>error</p>
		{/await}
	</div>
	


</main>

<style>
	body{
	background-image: url();
}
.pokedex{
	color: white;
	width: 200px;
	height: auto;
	background: red;
	border-radius: 10px 80px 10px 10px;
}
.searchbar{
	border-radius: 10px 20px 10px 10px;
}
.centerpokedex{
	margin: auto;
  	width: 400px;
  	border: 6px solid rgb(255, 101, 101);
  	padding: 10px;
	
	
}

</style>
