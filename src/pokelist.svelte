<script>
    import {createEventDispatcher} from 'svelte'; //??? https://qiita.com/sho_U/items/2d52590bd7973fbec671

    const dispatch = createEventDispatcher();

    export let pokemons =[]

    const handlePokemonClick = (pokemon) => {
        dispatch('selectPokemon',pokemon) //createeventのところにかかわっていそうやけど。よくわからん￥。多分ポケモンを選択できるっていう部分なきがするけど
    }

</script>

<ul>

    {#each pokemons as pokemon}<!-- https://learn.svelte.dev/tutorial/each-blocks  ポケモン毎に設定するんじゃなくて、pokemonで型作ってそれをポケモン毎に入れていく。-->
    <li>
        <button on:click="{() => handlePokemonClick(pokemon)}" ><!--pokemonに対してのbottton[pokemonname]でのトリガーの設定-->
            {pokemon.name}
        <button>
    </li>
    {/each}
</ul>