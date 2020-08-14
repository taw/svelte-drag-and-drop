<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let item;
  export let key;

  function ondragstart(event) {
    event.dataTransfer.setData("text/plain", "")
    dispatch("dragitemstart", {itemKey: key})
  }
</script>

<div draggable={true} on:dragstart={ondragstart}>{ item }</div>

<style>
  div {
    height: 64px;
    width: 64px;
    margin: 12px;
    padding: 12px;
    border: 2px solid black;
    background-color: #faa;
  }
</style>
