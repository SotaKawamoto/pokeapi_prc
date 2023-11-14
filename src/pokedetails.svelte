<script>
    export let pokemon
    //pokedetailsを使うためにpokelistのclickeventで選択されたselectedpokemon情報を取得し、pokemonに格納する
    //このときは、url?? {jsonデータを指すのか？}.はオブジェクトだろうけど.あと画像の切り替えもできてないけど、
    //defaultからofficial artworkとかの切り替えできない漢字なん？
    let promise
    $:promise = getPoke(pokemon.url)

    async function getPoke(url){
        const res = await fetch(pokemon.url);
        return await res.json();
    }

</script>

<style>
    <style>
    div {
        text-align: center;
        margin: 20px;
        display: flex;
        justify-content: center; /* 中央寄せ */
        align-items: center; /* 上下中央寄せ */
        height: 100vh; /* 画面の高さいっぱいに広がるように */
        flex-direction: column; /* 縦に並べる */
    }

    h2 {
        text-align: center;
        color: #333;
    }

    img {
        max-width: 100%; /* 画像の最大幅を設定 */
        height: auto; /* アスペクト比を保持しながら幅に合わせて調整 */
        margin-top: 10px; /* 画像とタイトルの間に余白を追加 */
    }
</style>


<div>
    {#await promise}
        searching {pokemon.name}
    {:then pokemonDetails}
        <h2>{pokemonDetails.name}</h2>
        <img src = {pokemonDetails.sprites.versions['generation-vii']['ultra-sun-ultra-moon'].front_default} alt={pokemonDetails.name} />
    {:catch error}
        Error
    {/await}
</div>