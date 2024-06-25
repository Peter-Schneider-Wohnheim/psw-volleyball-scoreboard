<script lang="ts">
    import { onMount, onDestroy } from "svelte";
    import Counter from "$lib/Counter.svelte";
    let counter1: any;
    let counter2: any;

    let maxPoints = 1;

    onMount(() => {
        maxPoints = Number(window.prompt("Maximum score", "21"));
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
                <Counter bind:this={counter1} on:reset={handleReset} maxPoints={maxPoints} />
        </div>
        <div class="col-6">
            <Counter bind:this={counter2} on:reset={handleReset} maxPoints={maxPoints}/>
        </div>
    </div>
</div>
<div class="text-center" style="height: 10vh;">
    <div class="row">
        <div class="col">
            <button type="button" class="btn btn-outline-secondary w-25 p-2" on:click={() => {counter1.reset(); counter2.reset();}}>New game</button>
        </div>
    </div>
</div>