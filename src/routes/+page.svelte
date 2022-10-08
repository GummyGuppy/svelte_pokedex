<script>

    import { loop_guard } from "svelte/internal";
    import "../app.css";
    import Button from '../components/Button.svelte'
    import Card from '../components/Card.svelte'

	
	$: currentPokemon = 1// 0
	$: pokemon = []
	
	let value = ''
		
	//fetch pokemon from PokeAPI
	function getPokemon(){
    
        let index = 0

		fetch("https://pokeapi.co/api/v2/pokemon?limit=151") //
			.then(response => response.json()) //
			.then(allpokemon =>  {
			allpokemon.results.map((poke) => 
            
                pokemon = [...pokemon, {
                    index: index++,
                    name: poke.name
                }]
                )})
                .then(() => console.log(pokemon))
                
	}	

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }

	//populate pokemon array on page load
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

    
    <h1 class="text-xl">
        {pokemon[0]}
    </h1>

    <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{currentPokemon}.png"
        class="w-48 h-48"/>
    <p>
       
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

