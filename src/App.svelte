<script>
   
    import pokelist from './pokelist.svelte'
    import pokeDetails from './pokedetails.svelte'
    let name;
    
    const promise = getPokemons();
    let selectedPokemon = null;

    async function getPokemons(){//非同期情報を得る関数の定義
        const res =await fetch('https://pokeapi.co/api/v2/pokemon')//name,urlの入ったデータを得ることができる？指定までか？
        const json =await res.json();//ここでjsonデータの入手か

        return json.results;// ここにresult:name,urlが入ってる
    }

    const selectPokemon= ({detail}) => {//アローはっていうのはみたいな感じ
        selectedPokemon = detail;
    }
</script>

<h1>
    Pokesearch
</h1>

<div>
    {#await promise}<!--非同期（この時name,urlのjson）データの確認-->
        searching pokemon
    {:then pokemons} <!--pokelist先のデータ？？pokemons??url先のjosnデータ関係の気がするけど中かっこは何-->
        <Pokelist pokemons={pokemons}　on:selectPokemon={selectePokemon} />
    

</div>
