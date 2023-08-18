<script>
    import { fade, fly } from 'svelte/transition'
    export let status = ''
    export let rank
    export let visible
    $: visible, setTimeout( () => { visible = false }, 2000)
</script>

<div class="alert-container">
    {#if visible}
    <div 
        class={status} 
        in:fly={{ y: -200, duration: 350}} 
        out:fly={{ y: -200, duration: 350}}>
        <p>
            {#if status === 'guessed-before'}
            Eliminated! {rank === 1101 ? `` : `#${rank} `}Already guessed ...
            {:else if status === 'success'}
            #{rank} Pass!
            {:else}
            {rank === 1101 ? `Name not found!` : `#${rank}`} Eliminated!
            {/if}
        </p>
    </div>
    {/if}
</div>

<style lang="scss">
.alert-container {
    position: absolute;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    div {
        height: fit-content;
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        font-size: 32px;
        text-align: center;
        color: white;
    }
    p {
        margin: 0;
        padding: 12px 24px;
    }
}
.guessed-before {
    background-color: rgb(156, 118, 24);
}
.success {
    background-color: rgb(59, 119, 31);
}
.fail {
    background-color: rgb(209, 104, 99);
}

</style>