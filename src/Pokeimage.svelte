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
<div class="accordion" id="accordionPanelsStayOpenExample">
	<div class="accordion-item">
	  <h2 class="accordion-header" id="panelsStayOpen-headingOne">
		<button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseOne" aria-expanded="true" aria-controls="panelsStayOpen-collapseOne">
		  {JSON.stringify(pokemondetails.sprite.key)}
		</button>
	  </h2>
	  <div id="panelsStayOpen-collapseOne" class="accordion-collapse collapse show" aria-labelledby="panelsStayOpen-headingOne">
		<div class="accordion-body">
			<img src="{pokemondetails.sprites.front_default}" alt="error">
		</div>
	  </div>
	</div>
	<div class="accordion-item">
	  <h2 class="accordion-header" id="panelsStayOpen-headingTwo">
		<button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseTwo" aria-expanded="false" aria-controls="panelsStayOpen-collapseTwo">
		  Accordion Item #2
		</button>
	  </h2>
	  <div id="panelsStayOpen-collapseTwo" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingTwo">
		<div class="accordion-body">
			<img src="{pokemondetails.sprites.front_shiny}" alt="error">
		</div>
	  </div>
	</div>
  </div>


{/await}
