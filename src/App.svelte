<script>
    import Searchbar from './searchbar.svelte'
    import Pokelist　from './pokelist.svelte'
    import PokeDetails from './pokedetails.svelte'
    import Pokechoose from './pokechoose.svelte';
    //props名の頭文字は大文字にしなくては認識してくれない
    //propertiesの頭文字は大文字にするのが命名規則
    //命名規則についてhttps://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions
    
    let q = 'kietemau'//これはsearchbarの中のinputのバリューだから変数じゃないいと定数には書き込めん
    let pokes =[];
    let empty = false

    const promise1 = getPokemons();//非同期処理の結果を表すオブジェクトがpromiseで、getpokemons()によって得た非同期情報を表す
    let selectedPokemon = null;

    // 非同期処理promiseオブジェクトの使い方in svelte　多分promiseのワードに意味があるのではなく、asyncでpromiseの意味になる？
    //　マークアップ側で｛#await promise｝ {:then pokemons} {:catch errot}みたいな感じで制御できる

    async function getPokemons(){//非同期情報を得る関数の定義
        const res =await fetch('https://pokeapi.co/api/v2/pokemon?limit=1017&&offset=0')//name,urlの入ったデータを得ることができる？指定までか？
        const json =await res.json();//ここでjsonデータの入手か

        return json.results;// ここにresult:name,urlが入ってる
    }

    /*const selectPokemon = ({detail}) => {//アローは”っていうのは”みたいな感じ
        selectedPokemon = detail;
    }*/



    const handleSubmit = () =>{
        let promise2 =choosepoke()
    }

    const choosepoke = async () => {//ポケモンの検索機能にしたい js6133
    pokes = []
    empty = false
    const result = await pokemons.get({ q })//getは何？？？ {q}を満たす個をgetする
    empty = result.totalItems === 0
    pokes = result.name
    }


</script>

<h1>
    Pokesearch
</h1>

<form>
    <Searchbar bind:value={q} />
    {q}
</form>
    
<div>
    

    {#await promise1}<!--非同期（この時name,urlのjson）データの確認-->
        searching pokemon
        
    {:then pokemons} <!--結局このpokemonsはユーザーが選べる変数でpromise１の結果が格納されるのか-->

    <!--pokelist先のpokemonsにpromiseの処理によって得られた非同期データ｛pokemon｝（json.result）を格納している。
    また、on:によってselectpokemon関数を結んでいる。
    selectpokemon関数内のselectpokemonはpokelistのbottonによるイベントで取得される変数かな？？マークアップ側で制御できるんや・・
    あとifの中身は真偽で使ってるて感じかな？selectedpokemonが存在する＝＞pokelist内で選択されているなら真-->

    <!--<Pokechoose pokemons={pokemons} pokes={selectPokemon} />-->   <!--カスタムイベントにpokesを設定しないとだめかも

        未だにonが分かってるとはいえないけど、pokes＝{selectPokemon関数で pokesの情報、
    つまりはpoklelistでいうボタンで選択されたpokemonの情報、pokechhohseでいうリンクの場所で入力で検索されたpokeの名前の情報} がselectedぽけもんに入力される
ただ、この順序よく分からん　-->
<!--    <Pokelist pokemons={pokemons}　on:selectPokemon={selectPokemon} /> 後ろの/>これの扱いは；みたいなもの -->
            {#await promise2}
            {:then selectedpokrmon}<!--thenの変数の方は開発者が定義？？　非同期操作が成功した場合に結果がその変数に格納される-->

        {#if selectedPokemon}
            <PokeDetails pokemon = {selectedPokemon} />
            {:else}
            not selected
        {/if}
        {/await}

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