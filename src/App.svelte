<script>
    import Searchbar from './searchbar.svelte'
    import PokeDetails from './pokedetails.svelte'
        
    let q = 'kietemau'
    let pokes =[];
    let empty = false

    let promise1 = getPokemons();
    let selectedPokemon = null;
    let promise2 = null;

    async function getPokemons(){
        const res =await fetch('https://pokeapi.co/api/v2/pokemon?limit=1017&&offset=0')
        const json =await res.json();
        /*console.log(json.results)　//リンク先からのjsonデータはキチンと取得できていた*/
        return json.results;
    }

    const handleSubmit = () =>{
        promise2 = choosepoke(promise1);
        console.log('promise2')
    }

    const choosepoke = async (pokemonsPromise) => {
        pokes = [];
        empty = false;

        try{
            const pokemons = await pokemonsPromise;
            /*console.log(pokemons)  //ポケモン　*/
            console.log({q})
            if(pokemons){
            const result = pokemons.filter(pokemon => pokemon.name === q)
            console.log(result)
            /*const result = await pokemons.get({ q })*/
            empty = result.length === 0
            const names = result.map(pokemon => pokemon.name);//pokemonオブジェクトの配列からpokemonオブジェクト内のnameプロパティの配列に変更
            pokes = names
            console.log(names)
            /*console.log(result.name)resultはnameプロパティを持つ検索されたオブジェくとの配列だからnameプロパティを持たない*/
            selectedPokemon = names;
            }         
        }catch(error){
            console.error(error)
        }
    }



</script>

<h1>
    Pokesearch
</h1>

<form on:submit|preventDefault={handleSubmit}>
    <Searchbar bind:value={q} />
    {q}
</form>
    
<div>

    {#await promise1}
        searching pokemon
    {:then pokemons} 
        {#if selectedPokemon}
            <PokeDetails pokemon = {selectedPokemon} />
        {:else}
            not selected
        {/if}
    {:catch error}
        error   
    {/await}
</div>    

<style>
    h1{
        text-align: center;
    }
    div{
        display: flex;
    }
</style>