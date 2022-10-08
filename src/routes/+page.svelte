<script>

    import "../app.css";
    import Button from '../components/Button.svelte'

	
	$: currentPokemon = 1// 0
	$: pokemon = []
	
	let value = ''
		
	//fetch pokemon from PokeAPI
	function getPokemon(){
		fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
			.then(response => response.json())
			.then(allpokemon =>  {
			allpokemon.results.map((poke) => pokemon = [...pokemon, poke.name])})
	
		
			
	}	
	//call function
	getPokemon()

	//back functionality
	function back(){
		if(currentPokemon > 1){
			currentPokemon--
		}
	}

	//next functionality
	function next(){
		if(currentPokemon < pokemon.length - 1)
			currentPokemon++
	}
	
</script>

<div class="flex flex-col w-screen gap-6 items-center">

    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{currentPokemon}.png"/>
    <p>
        current pokemon is {pokemon[currentPokemon - 1]}
    </p>

    <div class="flex gap-4">
        <Button fn={back} title="Back"/>
        <Button fn={next} title="Next"/>
    </div>



</div>


