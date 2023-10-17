<script>
    
const choosepoke = async ({pokemons}) => {//ポケモンの検索機能にしたい
    pokes = []
    empty = false
    const result = await pokemons.get({ q })//getは何？？？
    empty = result.totalItems === 0
    books = result.name
}
</script>