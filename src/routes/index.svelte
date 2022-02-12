<script lang="ts">
	import Board from '$lib/Board.svelte';

	let columnsData = [
		{
			id: 'c1',
			name: 'TODO',
			items: [
				{ id: 1, name: 'item41' },
				{ id: 2, name: 'item42' },
				{ id: 3, name: 'item43' },
				{ id: 4, name: 'item44' },
				{ id: 5, name: 'item45' },
				{ id: 6, name: 'item46' },
				{ id: 7, name: 'item47' },
				{ id: 8, name: 'item48' },
				{ id: 9, name: 'item49' }
			],
			scrollTop: 0
		},
		{
			id: 'c2',
			name: 'DOING',
			items: [
				{ id: 10, name: 'item50' },
				{ id: 11, name: 'item51' }
			],
			scrollTop: 0
		},
		{
			id: 'c3',
			name: 'DONE',
			items: [
				{ id: 13, name: 'item52' },
				{ id: 14, name: 'item53' },
				{ id: 15, name: 'item54' }
			],
			scrollTop: 0
		}
	];

	function handleBoardUpdated(newColumnsData) {
		columnsData = newColumnsData;
	}
</script>

<svelte:head>
	<title>Svelte Trello Clone</title>
</svelte:head>

<Board columns={columnsData} onFinalUpdate={handleBoardUpdated} />
