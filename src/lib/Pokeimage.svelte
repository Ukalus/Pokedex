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


<!-- Pokemon Characteristics -->
<div class="centercharacter container">
	<p class="container">No.{pokemondetails.id} {pokemondetails.name}</p>
	{#each pokemondetails.types as types }
	<p class="container">{types.type.name}</p>
	{/each}
	<div class="img pokeimg">
	<img src="{pokemondetails.sprites.front_default}" alt="error"> 
	</div>
	<p class="container">weight: {pokemondetails.weight} lbs</p>
	<p class="container">height: {pokemondetails.height} inches</p>
</div>
	<!-- Stats and Attacks -->
	<div class="accordion" id="accordionExample" style="color:black">
		<div class="accordion-item">
		<h2 class="accordion-header" id="headingOne">
			<button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="false" aria-controls="collapseOne">
			Stats
			</button>
		</h2>
		<div id="collapseOne" class="accordion-collapse collapse" aria-labelledby="headingOne" data-bs-parent="#accordionExample">
			<div class="accordion-body">
				{#each pokemondetails.stats as stats }
				<p>{stats.stat.name}:</p>
				<p>{stats.base_stat}:</p>
				{/each}
			</div>
		</div>
		</div>
		<div class="accordion-item">
		<h2 class="accordion-header" id="headingTwo">
			<button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
			Attacks
			</button>
		</h2>
		<div id="collapseTwo" class="accordion-collapse collapse" aria-labelledby="headingTwo" data-bs-parent="#accordionExample">
			<div class="accordion-body">
			<!-- All Moves -->
				{#each pokemondetails.moves as moves }
				<p>{moves.move.name}</p>
				{/each}
			</div>
		</div>
		</div>
	</div>
{/await}

<style>

p .centercharacter{
	border: 2px white;
}
.pokeimg{
	-webkit-transform: scaleX(-1);
	transform: scaleX(-1);
	background-color: white;
	width: 96px;
	border-radius: 50px;
	margin: 16px;
	border: 4px rgb(136, 136, 136);
}
.pokeimg:hover{
	-webkit-transform: scaleX(1);
	transform: scaleX(1);
	background-color: white;
	width: 96px;
	border-radius: 50px;
	margin: 16px;
}
</style>
