<nav>
    <a href = "/home">Home</a>
    <a href = "/file_talk">FileTalk</a>
</nav>

<style>
    .hover-effect {
        transition: all 0.3s ease;
    }
    .hover-effect:hover {
        transform: scale(1.2);
        background-color: #4CAF50; /* Change to your desired color */
    }
</style>

<!-- <h1 class="text-3xl font-bold underline">Welcome to SvelteKit</h1> -->


<body class="bg-black flex-col min-h-screen justify-center items-center">

    <div class="hover-effect bg-gray-800 p-6 rounded-lg flex flex-col items-center justify-center text-white font-bold text-lg cursor-pointer space-y-10">
        <a href = "/home">
        <p class="text-cyan-50 text-2xl rounded mb-2">
            
            Generate Robotic Voice
        </p>
        <span class="text-2xl">🤖</span>
        </a>
    </div>
    <div class="hover-effect bg-gray-800 p-6 rounded-lg flex flex-col items-center justify-center text-white font-bold text-lg cursor-pointer">
        <p class="text-cyan-50  text-2xl rounded mb-2">
            Generate Robotic Voice
        </p>
        <span class="text-2xl">🤖</span>
    </div>

</body>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
