<script>
	import Container from "./Container.svelte";

	let currentdrag = {};

	let data = [
		["A", "B", "C"],
		["D", "E", "F"],
	]

	function ondragend() {
		currentdrag = {};
	}

  function ondragitemend(event) {
		let {itemKey, sourceContainerKey} = currentdrag;
		let {targetContainerKey} = event.detail;
		let sourceContainer = data[sourceContainerKey];
		let targetContainer = data[targetContainerKey];
		let item = sourceContainer[itemKey];
		sourceContainer.splice(itemKey, 1)
		targetContainer.push(item)
		data = data;
  }

	function ondragitemstart(event) {
		currentdrag = event.detail;
  }
</script>

<div class="App">
	<header>
		Drag and Drop
	</header>
	{#each data as items, key }
		<Container {items} {key} on:dragitemstart={ondragitemstart} on:dragitemend={ondragitemend} />
	{/each}
</div>

<style>
	.App {
	  display: grid;
	  min-height: 100vh;
	  grid-template-rows: 100px 1fr;
	  grid-template-columns: 1fr 1fr;
	}

  header {
    font-size: 64px;
    text-align: center;
    grid-column: 1/3;
  }

  :global(.App .Container:nth-child(2)) {
    background-color: #aaf;
  }

  :global(.App .Container:nth-child(3)) {
    background-color: #afa;
  }
</style>
