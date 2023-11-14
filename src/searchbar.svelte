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
    height: 100vh;
    flex-direction: column;
  }

  .shadow {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .flex {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  input {
    text-align: center;
    margin: 20px;
    width: 80%;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 10px;
  }

  button {
    background-color: #fff;
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