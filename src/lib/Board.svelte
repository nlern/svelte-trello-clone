<script lang="ts">
	import { flip } from 'svelte/animate';
	import { fade } from 'svelte/transition';
	import { cubicIn } from 'svelte/easing';
	import { dndzone, SHADOW_ITEM_MARKER_PROPERTY_NAME } from 'svelte-dnd-action';
	import Column from './Column.svelte';

	export let columns;
	export let onFinalUpdate;

	const flipDurationMs = 300;

	function handleDndConsiderColumns(e) {
		onFinalUpdate(e.detail.items);
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
	use:dndzone={{
		items: columns,
		flipDurationMs,
		type: 'column'
	}}
	on:consider={handleDndConsiderColumns}
	on:finalize={handleDndFinalizeColumns}
>
	{#each columns as column, idx (column.id)}
		<div animate:flip={{ duration: flipDurationMs }} class="wrapper">
			<div class="column">
				<Column {column} onDrop={(newItems) => handleItemFinalize(idx, newItems)} />
				{#if column[SHADOW_ITEM_MARKER_PROPERTY_NAME]}
					<div in:fade={{ duration: 200, easing: cubicIn }} class="custom-shadow-item" />
				{/if}
			</div>
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
	.wrapper {
		height: 100%;
		flex: 0 0 272px;
	}
	.column {
		position: relative;
		height: 100%;
		padding: 0.5em;
		margin: 0.5em;
		background-color: #fff;
		border: 1px solid #333333;
	}

	.custom-shadow-item {
		position: absolute;
		top: 0; left:0; right: 0; bottom: 0;
		visibility: visible;
		border: 1px dashed grey;
		background: rgba(0, 0, 0, 0.5);
		opacity: 0.5;
		margin: 0;
	}
</style>
