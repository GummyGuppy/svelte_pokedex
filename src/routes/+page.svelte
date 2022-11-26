<script>

    import { loop_guard } from "svelte/internal";
    import "../app.css";
    import Button from '../components/Button.svelte'
    import Card from '../components/Card.svelte'


	$: currentPokemon = 0
    let pokemon = []
		
    
    //fetch on pageload ??
	fetch("https://pokeapi.co/api/v2/pokemon")
        .then(response => response.json())
        .then(res => res.results.forEach((pokemon) => {

            pokemon = [...pokemon, {
                name: pokemon.name,
                sprite: fetchPokemonData(pokemon)
            }]
            
        }))
            

    function fetchPokemonData(pokemon){
        let url = pokemon.url

        fetch(url)
        .then(res => res.json())
        .then(details => {
            console.log(details.sprites.front_shiny)
        })
    }

    function capitalizeFirstLetter(string) {
        return string.charAt(0).toUpperCase() + string.slice(1);
    }

	//back functionality
	function back(){
		if(currentPokemon > 0){
			currentPokemon--
		}
	}

	//next functionality
	function next(){
		if(currentPokemon < pokemon.length - 1)
			currentPokemon++
	}
	

//     {pokemon[currentPokemon]?.name}

// <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{currentPokemon + 1}.png"
//     class="w-48 h-48"/>
</script>

<div class="flex flex-col w-screen h-screen justify-center gap-6 items-center">

    <Card name={pokemon[currentPokemon]?.name}/>


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

