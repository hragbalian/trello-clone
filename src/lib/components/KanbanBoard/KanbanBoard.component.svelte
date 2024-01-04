<script lang="ts">
	import Column from './Column.component.svelte';
	import { kanbanStore } from '$lib/store';
	import type { KanbanBoardData } from '$types/kanban';
	import { onDestroy } from 'svelte';

	let kanbanData: KanbanBoardData;

	const unsub = kanbanStore.subscribe((store) => {
		kanbanData = store.kanbanBoard;
	});

	onDestroy(unsub);
</script>

{#if kanbanData}
	<section class="wrapper flex">
		<div class="flex w-full ml-10 flex-col gap-4 md:flex-row rounded-lg border-4">
			{#each Object.entries(kanbanData) as [columnId, entry]}
				<Column title={entry.columnName} tasks={entry.tasks} {columnId} />
			{/each}
		</div>
	</section>
{/if}

<style lang="scss">
	.wrapper {
		height: calc(100vh - 9rem);
		// width:100%
		overflow-x: auto;
		// width: calc(100vw - 1vw);
	}
</style>
