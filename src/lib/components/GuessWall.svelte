<script>
    import { fade } from 'svelte/transition'
    export let guesses
</script>

<div class="guess-container">
{#each guesses as guess}
    <div transition:fade={{duration: 350}} class={guess.correct ? 'correct' : 'false'}>{guess.name}</div> 
{/each}
</div>

<style lang="scss">
.guess-container {
    position: absolute;
    display: flex;
    flex-direction: row-reverse;
    justify-content: flex-start;
    align-items: flex-end;
    flex-wrap: wrap-reverse;
    align-content: flex-start;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    text-transform: uppercase;
    .correct {
        color: rgb(59, 119, 31);
    }
    .false {
        color: rgb(209, 104, 99);
    }
    div {
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        font-size: 22px;
        padding: 0px 4px;
        opacity: .5
    }
}
</style>