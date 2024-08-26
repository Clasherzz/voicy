<script lang="ts">
    // import { vitePreprocess } from "@sveltejs/vite-plugin-svelte";

    let prompt:string;
    let pitch:number = 50;
    let rate:number = 50;
    $:console.log(prompt);
    $:console.log(rate);
    $:console.log(pitch);

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
            message.pitch = pitch; // Set pitch, range 0 to 2
            message.rate = rate; // Set rate, range 0.1 to 10
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
<body class="bg-black text-white min-h-screen">
 

<div class="bg-black text-white p-4 rounded border border-white">
    <p class = "bg-green">Hey there</p>
    <!-- <label>Frequency</label> -->

    <input type="text" placeholder="Enter your text" bind:value={prompt} >
    <input type="range" bind:value={pitch} min=0 max=100>
    <!-- <input type="range" bind:value={} min="0" max="100" value="50"> -->
    <input type="range" bind:value={rate} min=0 max=100> 
    <button on:click={makeVoice} >Click me</button>
    <button on:click={()=>window.speechSynthesis.pause}>Pause</button>
    <button on:click={()=>window.speechSynthesis.resume}>Resume</button>
</div>
</body>
