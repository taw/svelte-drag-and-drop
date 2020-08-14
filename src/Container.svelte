<script>
  import Item from "./Item.svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let items;
  export let key;

  function ondrop(e) {
    dispatch("dragitemend", {targetContainerKey: key});
  }

  function ondragitemstart(event) {
    dispatch("dragitemstart", {...event.detail, sourceContainerKey: key});
  }
</script>

<div class="Container"
  on:dragover|preventDefault
  on:dragenter|preventDefault
  on:drop={ondrop}
>
  {#each items as item, key}
    <Item {item} {key} on:dragitemstart={ondragitemstart} />
  {/each}
</div>

<style>
</style>
