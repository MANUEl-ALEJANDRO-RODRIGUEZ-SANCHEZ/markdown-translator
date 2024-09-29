<template>
    <div class="container-fluid d-flex flex-column align-items-center justify-content-center vh-100">
      <div class="translator-box w-100 d-flex justify-content-between">
        <!-- Markdown Input -->
        <div class="input-section w-50 me-2">
          <h2>Escribe en Markdown</h2>
          <textarea
            v-model="markdownText"
            placeholder="Escribe o pega tu código Markdown aquí..."
            class="form-control"
          ></textarea>
        </div>
  
        <!-- Translated Output -->
        <div class="output-section w-50 ms-2">
          <h2>Salida HTML</h2>
          <div class="output border p-3 rounded" v-html="renderedMarkdown"></div>
        </div>
      </div>
  
      <div class="buttons mt-4">
        <button class="btn btn-danger me-2" @click="reset" :disabled="isTextareaEmpty">Resetear</button>
        <button class="btn btn-success me-2" @click="downloadMarkdown" :disabled="isTextareaEmpty">Descargar como .md</button>
        <button class="btn btn-primary" @click="downloadHTML" :disabled="isTextareaEmpty">Descargar como HTML</button>
      </div>
    </div>
  </template>
  
  <script>
  import { marked } from 'marked';
  
  export default {
    data() {
      return {
        markdownText: '',
      };
    },
    computed: {
      renderedMarkdown() {
        return marked(this.markdownText, { sanitize: true });
      },
      isTextareaEmpty() {
        return this.markdownText.trim() === ''; 
      },
    },
    methods: {
      reset() {
        if (this.isTextareaEmpty) {
          alert("El textarea está vacío, no se puede resetear.");
          return;
        }
        this.markdownText = '';
      },
      downloadMarkdown() {
        if (this.isTextareaEmpty) {
          alert("El textarea está vacío, no puedes descargar.");
          return;
        }
        const blob = new Blob([this.markdownText], { type: 'text/markdown' });
        this.downloadFile(blob, 'document.md');
      },
      downloadHTML() {
        if (this.isTextareaEmpty) {
          alert("El textarea está vacío, no puedes descargar.");
          return;
        }
        const blob = new Blob([this.renderedMarkdown], { type: 'text/html' });
        this.downloadFile(blob, 'document.html');
      },
      downloadFile(blob, filename) {
        const link = document.createElement('a');
        link.href = URL.createObjectURL(blob);
        link.download = filename;
        link.click();
      },
    },
  };
  </script>

<style scoped>
.container {
  max-width: 1200px;
  text-align: center;
}

.container-fluid{
    padding: 10%;
}

h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

textarea {
  height: 400px;
}

.output {
  min-height: 400px;
  background-color: #f9f9f9;
}

/* Estilos para el tema oscuro */
body.dark-theme .container-fluid{
  background-color: #2F3438;
  color: #f1f1f1;
}

body.dark-theme textarea {
  background-color: #1e1e1e;
  color: #fff;
}

body.dark-theme textarea::placeholder{
    color: #fff;
}

body.dark-theme .output {
  background-color: #1e1e1e;
  color: #fff;
  border-color: #555;
}

/* body.dark-theme .btn {
  background-color: #555;
}

body.dark-theme .btn:hover {
  background-color: #333;
} */

.buttons {
  margin-top: 20px;
}

button {
  font-size: 1.1em;
  cursor: pointer;
}
</style>
