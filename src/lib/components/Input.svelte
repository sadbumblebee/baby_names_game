<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()

    export let value = "Guess a name ..."

    const submit = () => {
        dispatch('submit')
        value = ''
    }
</script>

<div class='form-container'>
<form on:submit|preventDefault={ () => submit}>
    <input autocomplete="off" id="input-guess" class="animation" bind:value={value}/>
    <button class="button" on:click={submit}>🐣</button>
</form>
</div>

<style lang="scss">
.form-container {
    width: 100%;
    height: 100vh;
    position: relative;
    z-index: 100;
    // background-color:pink;
    display: flex;
    align-items: center;
    justify-content: center;
}

form {
    display: flex;
    align-items: flex-end;
    padding: 24px 24px;
    border-radius: 24px;
    background-color: rgba(255,255,255, .75);
    box-shadow: 0px 0px 12px rgba(255,255,255, .75);
    input, .button {
        font-weight: 400;
        font-size: 32px;
        height: 50px;
    }
}

input {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    margin-right: 20px;
    width: 100%;
    transition: 0.6s;
    border: none;
    border-bottom: 2px solid lightgray;
    background-color: transparent;
    &:focus, &:hover {
        outline: none;
        border-bottom: 2px solid black;
    }
}

.button {
    background: none;
	color: inherit;
	border: none;
	padding: 0;
	font: inherit;
	cursor: pointer;
	outline: inherit;
    flex: 0 1 auto;
    align-self: auto;
    cursor: pointer;
    transition: transform 150ms cubic-bezier(0.64, 0.57, 0.67, 1.53);
    &:hover {
        transform: rotate(-20deg);
    }
}

</style>