<script lang="ts">
	import { flip } from 'svelte/animate';
	import { dndzone } from 'svelte-dnd-action';
	import Column from './Column.svelte';

	export let columns;
	export let onFinalUpdate;

	const flipDurationMs = 300;

	function handleDndConsiderColumns(e) {
		columns = e.detail.items;
	}

	function handleDndFinalizeColumns(e) {
		onFinalUpdate(e.detail.items);
	}

	function handleItemFinalize(columnIdx, newItems) {
		columns[columnIdx].items = newItems;
		onFinalUpdate([...columns]);
	}
</script>

<section
	class="board"
	use:dndzone={{ items: columns, flipDurationMs, type: 'column' }}
	on:consider={handleDndConsiderColumns}
	on:finalize={handleDndFinalizeColumns}
>
	{#each columns as { id, name, items }, idx (id)}
		<div class="column" animate:flip={{ duration: flipDurationMs }}>
			<Column {name} {items} onDrop={(newItems) => handleItemFinalize(idx, newItems)} />
		</div>
	{/each}
</section>

<style>
	.board {
		height: 90vh;
		width: 100%;
		padding: 0.5em;
		display: flex;
		flex-direction: row;
		gap: 0.5rem;
	}
	.column {
		height: 100%;
		flex: 0 0 272px;
		padding: 0.5em;
		margin: 0.5em;
		background-color: #fff;
		border: 1px solid #333333;
	}
</style>
