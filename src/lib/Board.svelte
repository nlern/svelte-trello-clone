<script lang="ts">
	import Column from './Column.svelte';
	const lists = [
		{
			id: 1,
			title: 'Notes / New Ideas',
			cards: [
				{
					id: 1,
					title: "Legacy metric's officer",
					description: 'lorem ipsum'
				},
				{
					id: 2,
					title: "Product security producer",
					description: 'lorem ipsum'
				}
			]
		},
		{
			id: 2,
			title: 'Projects',
			cards: []
		},
		{
			id: 3,
			title: "Today's tasks",
			cards: []
		},
		{
			id: 4,
			title: 'Future tasks',
			cards: []
		},
		{
			id: 5,
			title: 'Waiting for input',
			cards: []
		},
		{
			id: 6,
			title: 'Completed',
			cards: []
		}
	];
</script>

<section class="board">
	{#each lists as list (list.id)}
		<Column {list} />
	{/each}
</section>

<style>
	.board {
		display: flex;
		flex-direction: row;
		gap: 0.5rem;
	}
</style>
