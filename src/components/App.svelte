<script>
  import { onMount } from "svelte";
  const API = "https://rickandmortyapi.com/api/character";
  let data = [];
  let characters = [];
  onMount(async () => {
    const res = await fetch(API);
    data = await res.json();
    characters = data.results;
  });
</script>

<style>
  .characters {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 8px;
  }
  figure,
  img {
    width: 100%;
    margin: 0;
  }

  @media screen and ( max-width: 960px ) {
    .characters {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  @media screen and ( max-width: 650px ) {
    .characters {
      grid-template-columns: repeat(1, 1fr);
    }
  }

</style>

<div class="characters">
  {#each characters as character}
    <figure>
      <img src={character.image} alt={character.name} />
      <figcaption>{character.name}</figcaption>
    </figure>
  {:else}
    <p>loading...</p>
  {/each}
</div>