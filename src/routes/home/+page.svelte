<script lang="ts">
    let prompt: string = '';
    let pitch: number = 50;
    let rate: number = 50;
    let voices: SpeechSynthesisVoice[] = [];
    let isSpeaking: boolean = false;

    function getAllVoices() {
        if ('speechSynthesis' in window) {
            voices = window.speechSynthesis.getVoices();
            console.log(voices);
        } else {
            console.error("Speech Synthesis not supported.");
        }
    }

    function makeVoice() {
        if ('speechSynthesis' in window && prompt) {
            const message = new SpeechSynthesisUtterance(prompt);
            if (voices.length > 0) {
                message.voice = voices[0]; // Use the first available voice
            }
            message.pitch = pitch / 50; // Adjust pitch, range 0 to 2
            message.rate = rate / 50; // Adjust rate, range 0.1 to 2
            isSpeaking = true;
            window.speechSynthesis.speak(message);
            
            message.onend = () => {
                isSpeaking = false;
            };
        } else {
            console.error("Speech Synthesis not supported or prompt is empty.");
        }
    }

    // Ensure voices are loaded before trying to use them
    window.speechSynthesis.onvoiceschanged = () => {
        getAllVoices();
    };

    // Initialize voices on script load
    getAllVoices();
</script>

<style>
    @keyframes pulse {
        0% {
            transform: scale(1);
            opacity: 1;
        }
        50% {
            transform: scale(1.2);
            opacity: 0.7;
        }
        100% {
            transform: scale(1.5);
            opacity: 0;
        }
    }

    .circle-animation {
        animation: pulse 1.5s infinite;
    }
</style>

<body class="bg-black text-white min-h-screen flex justify-center items-center">
    <div class="bg-gray-900 text-white p-6 rounded-lg border border-white space-y-4">
        <!-- <p class="bg-green-500 p-2 rounded-md">Hey there</p> -->
        <input type="text" placeholder="Enter your text" bind:value={prompt} class="w-full p-2 text-black rounded-md">
        
        <div class="flex space-x-4 items-center">
            <label class="font-serif">Pitch</label>
            <input type="range" bind:value={pitch} min="0" max="100" class="w-full">
        </div>
        
        <div class="flex space-x-4 items-center">
            <label class="font-serif">Rate</label>
            <input type="range" bind:value={rate} min="0" max="100" class="w-full">
        </div>
        
        <div class="flex space-x-4">
            <button on:click={makeVoice} class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Click me</button>
            <button on:click={() => window.speechSynthesis.pause()} class="bg-yellow-500 hover:bg-yellow-700 text-white font-bold py-2 px-4 rounded">Pause</button>
            <button on:click={() => window.speechSynthesis.resume()} class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded">Resume</button>
        
        </div>
        
        <div class="relative flex justify-center items-center w-36 h-36 mx-auto mt-6">
            <!-- Animated Outer Circle -->
            {#if isSpeaking}
                <div class="absolute w-full h-full bg-gray-500 rounded-full circle-animation"></div>
            {/if}
            <!-- Speaker Emoji in the Center -->
            <span class="text-5xl">🔊</span>
        </div>
    </div>
</body>
