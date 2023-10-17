<script>
   
    import Pokelist　from './pokelist.svelte'
    import PokeDetails from './pokedetails.svelte'
    //props名の頭文字は大文字にしなくては認識してくれない
    //propertiesの頭文字は大文字にするのが命名規則
    //命名規則についてhttps://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions
    

    let name;
    
    const promise = getPokemons();//非同期処理の結果を表すオブジェクトがpromiseで、getpokemons()によって得た非同期情報を表す
    let selectedPokemon = null;

    // 非同期処理promiseオブジェクトの使い方in svelte　
    //　マークアップ側で｛#await promise｝ {:then pokemons} {:catch errot}みたいな感じで制御できる

    async function getPokemons(){//非同期情報を得る関数の定義
        const res =await fetch('https://pokeapi.co/api/v2/pokemon?limit=1017&&offset=0')//name,urlの入ったデータを得ることができる？指定までか？
        const json =await res.json();//ここでjsonデータの入手か

        return json.results;// ここにresult:name,urlが入ってる
    }

    const selectPokemon= ({detail}) => {//アローは”っていうのは”みたいな感じ
        selectedPokemon = detail;
    }
</script>

<h1>
    Pokesearch
</h1>

<div>
    {#await promise}<!--非同期（この時name,urlのjson）データの確認-->
        searching pokemon
    {:then pokemons} 
        <!--pokelist先のpokemonsにpromiseの処理によって得られた非同期データ｛pokemon｝（json.result）を格納している。
        また、on:によってselectpokemon関数を結んでいる。
        selectpokemon関数内のselectpokemonはpokelistのbottonによるイベントで取得される変数かな？？マークアップ側で制御できるんや・・
        あとifの中身は真偽で使ってるて感じかな？selectedpokemonが存在する＝＞pokelist内で選択されているなら真-->
        <Pokelist pokemons={pokemons}　on:selectPokemon={selectPokemon} />
        {#if selectedPokemon}
            <PokeDetails pokemon = {selectedPokemon} />
        {:else}
            not selected
        {/if}    
    {:catch error}
        {error.message}
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
