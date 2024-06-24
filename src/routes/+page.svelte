<script lang="ts">
    import { onMount, onDestroy } from "svelte";
    import Counter from "$lib/Counter.svelte";
    let counter1: any;
    let counter2: any;

    onMount(() => {
        counter1.reset();
        counter2.reset();

        const handleKeyUp = (event: KeyboardEvent) => {
            if (event.key === 'ArrowUp') {
                counter1.increment();
            } else if (event.key === 'ArrowDown') {
                counter2.increment();
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
</script>
<div class="d-flex align-items-center justify-content-center" style="height: 90vh;">
    <div class="row">
        <div class="col-6">
                <Counter bind:this={counter1} on:reset={handleReset} />
        </div>
        <div class="col-6">
            <Counter bind:this={counter2} on:reset={handleReset} />
        </div>
    </div>
</div>
<div class="text-center" style="height: 10vh;">
    <div class="row">
        <div class="col">
            <button type="button" class="btn btn-outline-secondary w-25 p-2" on:click={() => {counter1.reset(); counter2.reset();}}>Neues Spiel</button>
        </div>
    </div>
</div>