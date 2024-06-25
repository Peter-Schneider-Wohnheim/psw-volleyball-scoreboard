<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    let counter = 0;
    export let maxPoints = 1;

    export function increment(){
        if (counter < maxPoints) {
            counter += 1;
        }
    }

    export function decrement(){
        if (counter > 0) {
            counter -= 1;
        }
    }

    export function reset() {
        counter = 0;
        dispatch('reset');
    }
</script>

<div class="text-center">
    <button type="button" class="btn btn-outline-secondary w-25" on:click={() => increment()}>+</button>
    <h3 style="font-size: 30rem; padding-left: 10vb; padding-right: 10vb; width: 40rem;">{counter}</h3>
    <button type="button" class="btn btn-outline-secondary w-25" on:click={() => decrement()}>-</button>
</div>
