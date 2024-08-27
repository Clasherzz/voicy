<!-- 
<script>
    // function parseFile() {
    //         const fileInput = document.getElementById('fileInput');
    //      //   const output = document.getElementById('output');
    //         const file = fileInput.files[0];

    //         if (file) {
    //             const reader = new FileReader();
    //             reader.onload = function(event) {
    //                 const fileContent = event.target.result;
    //               //  output.textContent = fileContent;
    //             };

    //             reader.onerror = function(event) {
    //                // output.textContent = "Error reading file!";
    //                console.log("error here");
    //             };

    //             reader.readAsText(file); // Reads the file as plain text
    //         } else {
    //             output.textContent = "No file selected!";
    //         }
    //     }
    import '../../app.css';

</script>
<input type="file" id="fileInput">
<h class="font-bold underline">hello</h>
<button onclick="parseFile()">Upload and Parse</button> -->
<script>
    let fileContent = '';
    let dragOver = false;
  
    // Handle file selection via click
    const handleFileSelect = (event) => {
      const file = event.target.files[0];
      if (file) {
        readFile(file);
      }
    };
  
    // Handle file drop
    const handleDrop = (event) => {
      event.preventDefault();
      const file = event.dataTransfer.files[0];
      if (file) {
        readFile(file);
      }
      dragOver = false; // Reset dragOver state
    };
  
    // Read file content
    const readFile = (file) => {
      const reader = new FileReader();
      reader.onload = () => {
        fileContent = reader.result;
      };
      reader.readAsText(file);
    };
  
    // Handle drag over event
    const handleDragOver = (event) => {
      event.preventDefault();
      dragOver = true; // Set dragOver state
    };
  
    // Handle drag leave event
    const handleDragLeave = (event) => {
      dragOver = false; // Reset dragOver state
    };
  </script>
  
  <style>
    .drop-area {
      border: 2px dashed #ccc;
      padding: 20px;
      text-align: center;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .drop-area.drag-over {
      background-color: #f0f8ff;
      border-color: #0b76ef;
    }
  </style>
  
  <div
    class="drop-area {dragOver ? 'drag-over' : ''}"
    on:click={() => document.getElementById('fileInput').click()}
    on:dragover={handleDragOver}
    on:dragleave={handleDragLeave}
    on:drop={handleDrop}
  >
    <p>Click or drag and drop a file here to upload</p>
  </div>
  
  <input
    type="file"
    id="fileInput"
    style="display: none;"
    on:change={handleFileSelect}
  />
  
  {#if fileContent}
    <h3>File Content:</h3>
    <pre>{fileContent}</pre>
  {/if}
  