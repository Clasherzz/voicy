<script lang="ts">
    // import { vitePreprocess } from "@sveltejs/vite-plugin-svelte";

    let prompt:string;
    $:console.log(prompt);

    function pressed() {
        if ('speechSynthesis' in window) {
            console.log("Speech Synthesis supported.");
        } else {
            console.log("Speech Synthesis not supported.");
        }
    }

    function getAllVoices() {
        if ('speechSynthesis' in window) {
            const voices = window.speechSynthesis.getVoices();
            console.log(voices); // Now it correctly logs the voices
            return voices;
        } else {
            console.error("Speech Synthesis not supported.");
            return [];
        }
    }

    function makeVoice() {
        if ('speechSynthesis' in window) {
            const message = new SpeechSynthesisUtterance(prompt);
            const voices = getAllVoices();
            if (voices.length > 0) {
                message.voice = voices[0]; // Use the first available voice
            }
            message.pitch = 1; // Set pitch, range 0 to 2
            message.rate = 1; // Set rate, range 0.1 to 10
            window.speechSynthesis.speak(message);
        } else {
            console.error("Speech Synthesis not supported.");
        }
    }

    // Ensure voices are loaded before trying to use them
    window.speechSynthesis.onvoiceschanged = () => {
        console.log("Voices changed, available voices:", getAllVoices());
    };
</script>

<div>
    <p>Hey there</p>
    <!-- <label>Frequency</label> -->

    <input type="text" placeholder="Enter your text" bind:value={prompt} >
    <input type="range" min="0" max="100" value="50">
    <button on:click={makeVoice}>Click me</button>
</div>
