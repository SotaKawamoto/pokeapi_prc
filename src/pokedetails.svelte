<script>
    export let pokemon
    //pokedetailsを使うためにpokelistのclickeventで選択されたselectedpokemon情報を取得し、pokemonに格納する
    //このときは、url?? {jsonデータを指すのか？}.はオブジェクトだろうけど.あと画像の切り替えもできてないけど、
    //defaultからofficial artworkとかの切り替えできない漢字なん？
    let promise
    $:promise =getpoke(pokemon.url)

    async function getpoke(url){
        const res = await fetch(pokemon.url);
        return await res.json();
    }

</script>

<div>
    {#await promise}
        searching {pokemon.name}
    {:then pokemonDetails}
        <h2>{pokemonDetails.name}</h2>
        <img src = {pokemonDetails.sprites.front_default} alt={pokemonDetails.name} />
    {:catch error}
        Error
    {/await}
</div>