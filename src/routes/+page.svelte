<script>

    import { loop_guard } from "svelte/internal";
    import "../app.css";
    import Button from '../components/Button.svelte'
    import Card from '../components/Card.svelte'


	let currentPokemon = 0
    $: allPokemon = []
    let sprites = []
		
    
    //fetch on pageload ??
	fetch("https://pokeapi.co/api/v2/pokemon?limit=151")
        .then(response => response.json())
        .then(res => res.results.forEach(poke => {
  
           fetchPokemonData(poke)
  
    }))
    
            

    function fetchPokemonData(pokemon){

        let url = pokemon.url

        fetch(url)
        .then(res => res.json())
        .then(details => {

             console.log("Name is: " + details.name)
            console.log("sprites are " + JSON.stringify(details.sprites))

           allPokemon = [...allPokemon, details.name]
           sprites = [...sprites, details.sprites.front_default]
           
           

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
		if(currentPokemon < allPokemon.length - 1)
			currentPokemon++
	}
	
</script>

<div class="flex flex-col w-screen h-screen justify-center gap-6 items-center">

    {#if !allPokemon[currentPokemon]}
        <h1>loading...</h1> 
        {:else}
        <h1 class="text-2xl">{allPokemon[currentPokemon]}</h1>
        <img src={sprites[currentPokemon]} class="w-48 h-48">
    {/if}
    
    

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

