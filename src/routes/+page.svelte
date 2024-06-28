<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import Counter from '$lib/Counter.svelte';

	let counter1: any;
	let counter2: any;
	let showModal: boolean = true;

	let maxPoints = 25;

	onMount(() => {
		counter1.reset();
		counter2.reset();

		const handleKeyUp = (event: KeyboardEvent) => {
			if (event.key === 'PageUp') {
				counter1.increment();
			} else if (event.key === 'PageDown') {
				counter2.increment();
			} else if (event.key === 'b') {
				counter1.reset();
				counter2.reset();
			}
		};

		window.addEventListener('keyup', handleKeyUp);

		return () => {
			window.removeEventListener('keyup', handleKeyUp);
		};
	});

	function handleReset() {
		console.log('Counter has been reset');
	}

	function handleModalSubmit() {
		showModal = false;
		counter1.reset();
		counter2.reset();
	}
</script>
<div class="d-flex align-items-center justify-content-center" style="height: 100vh;">
	<div class="row">
		<div class="col-6">
			<Counter bind:this={counter1} on:reset={handleReset} maxPoints={maxPoints} />
		</div>
		<div class="col-6">
			<Counter bind:this={counter2} on:reset={handleReset} maxPoints={maxPoints} />
		</div>
	</div>
</div>
<button type="button"
				class="btn btn-primary new-game-btn"
				on:click={() => {counter1.reset(); counter2.reset();}}>
	<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-clockwise" viewBox="0 0 16 16">
		<path fill-rule="evenodd" d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2z"/>
		<path d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466"/>
	</svg>
</button>

<!-- Bootstrap Modal -->
{#if showModal}
	<div class="modal fade show d-block" tabindex="-1">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h5 class="modal-title">Set Maximum Score</h5>
					<button type="button" class="btn-close" aria-label="Close" on:click={() => showModal = false}></button>
				</div>
				<div class="modal-body">
					<input type="number" class="form-control" bind:value={maxPoints} min="1">
				</div>
				<div class="modal-footer">
					<button type="button" class="btn btn-primary" on:click={handleModalSubmit}>Set max score</button>
				</div>
			</div>
		</div>
	</div>
	<div class="modal-backdrop fade show"></div>
{/if}

<style>
    .new-game-btn {
        position: fixed;
        bottom: 20px;
        right: 20px;
				width: 50px;
				height: 50px;
				border-radius: 100%;
    }
</style>