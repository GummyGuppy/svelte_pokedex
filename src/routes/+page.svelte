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

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
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

<div class="flex flex-col w-screen h-screen justify-center gap-6 items-center">

    <h1 class="text-xl">{pokemon[currentPokemon - 1]}</h1>
    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{currentPokemon}.png"/>
    <p>
        current pokemon is {pokemon[currentPokemon - 1]}
    </p>

    <div class="flex gap-4">
        <Button fn={back} title="Back"/>
        <Button fn={next} title="Next"/>
    </div>



</div>

<style>
    h1::first-letter {
        text-transform:capitalize;
    }
    
</style>

