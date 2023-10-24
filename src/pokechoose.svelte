<script>
    export let pokemons=[];
    let pokemon =pokemons;
const choosepoke = async () => {//ポケモンの検索機能にしたい js6133
    pokes = []
    empty = false
    const result = await pokemons.get({ q })//getは何？？？ 
    empty = result.totalItems === 0
    pokes = result.name
}//このライブラリ？？他ファイルに分けるやり方をすると、polelistのselectpokemonみたいにうまくmain側のファイルでpokesが認識されない

const getBooks = async () => {
    books = []
    empty = false
    const result = await pokemon.get({ q })
    empty = result.totalItems === 0
    books = result.items
  }
</script> 