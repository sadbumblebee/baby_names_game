<script>
import Alert from '$lib/components/Alert.svelte'
import Input from '$lib/components/Input.svelte'
import GuessWall from '$lib/components/GuessWall.svelte'
import allData from '$lib/data.json'
const data = allData.slice(0,50)

let name
let guesses = []
let status
let rank = null
let visible = false

const handleSubmit = () => {
    // Check names existence
    checkNameSubmission(name)
}

const checkTopKRank = (name) => {
    const mName = allData.filter( el => el.male.toLowerCase() === name.toLowerCase())
    const fName = allData.filter( el => el.female.toLowerCase() === name.toLowerCase())
    // Get rank
    const rank = mName.length == 0 ? fName.length == 0 ? 1101 : fName[0].rank : mName[0].rank
    return rank
}

const checkNameSubmission = (name) => {
    // Check top 100
    const mName = data.filter( el => el.male.toLowerCase() === name.toLowerCase())
    const fName = data.filter( el => el.female.toLowerCase() === name.toLowerCase())

    // If name has been guessed already!
    if (checkGuesses(name)) {
        // Fail message Guessed already!
        console.log("Guessed already!")
        rank = checkTopKRank(name)
        status = 'guessed-before'
        visible = true
        return
    }
    // If the name doesn't exist
    else if (mName.length == 0 && fName.length == 0) {
        // Fail message
        rank = checkTopKRank(name)
        console.log("Name not found")
        status = 'fail'
        visible = true
        // Add name to guess list
        storeGuess(name, false)
    } else {
        rank = mName.length == 0 ? fName[0].rank : mName[0].rank
        // Success message
        console.log("Name found")
        status = 'success'
        visible = true
        // Add name to guess list
        storeGuess(name, true)
    }
}

// Check if guesses exist
const checkGuesses = (name) => { 
    return guesses.some( guess => guess.name.toLowerCase() === name.toLowerCase()) 
}

// Store guesses
const storeGuess = (name, correct) => {
    guesses = [...guesses, {name: name, correct: correct}]
}

</script>

<!-- HTML -->
<div class='main'>
<Alert {rank} {status} bind:visible={visible}/>
<Input bind:value={name} on:submit={handleSubmit} />
<GuessWall {guesses} />
</div>

<!-- Style -->
<style global lang="scss">
// @import 'sanitize.css';

.main {
    position: relative;
    width: 100%;
    height: 100%;
    object-fit: contain;
}
</style>