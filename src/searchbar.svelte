<script>
  export let value ='';//textinputのチュートリアルのようにexport側の値もinputをバインドすればOK？
</script>

<style>
  div {
    text-align: center;
    margin: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 20%;
    width:100%;
    background-color: #070807;
    flex-direction: column;
  }

  .shadow {
    box-shadow: 0 4px 8px #0000001a;
  }

  .flex {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  input {
    text-align: center;
    margin: 20px;
    width: 20%;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 10px;
  }

  button {
    background-color: #a3bbad;
    cursor: pointer;
    padding: 10px;
  }
</style>

<div>
  <div class="shadow flex">
      <input bind:value={value} class="w-full rounded p-2" type="text" placeholder="Search...">
      <button class="bg-white w-auto flex justify-end items-center text-blue-500 p-2 hover:text-blue-400">
        <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" class="w-6 h-6">
          <path d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
        </svg>
        検索
      </button>
  </div>
</div>