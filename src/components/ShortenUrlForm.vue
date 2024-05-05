<template>
  <div>
    <h1>URL Shortener</h1>
    <form @submit.prevent="shortenUrl">
      <label for="longUrl">Enter URL: </label>
      <input type="text" id="longUrl" v-model="longUrl" required>
      <br/>
      <button type="submit" class="margin-top-20">Shorten URL</button>
    </form>
    <a class="margin-top-20" :href="shortenedUrl" target="_blank">
        {{ shortenedUrl }}
    </a>
    <p v-if="error">{{ error }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      longUrl: '',
      shortenedUrl: '',
      error: ''
    };
  },
  methods: {
    shortenUrl() {
      fetch('http://localhost:8080/url', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ longUrl: this.longUrl })
      })
        .then(response => {
          if (response.ok) {
            return response.text();
          } else {
            throw new Error('Failed to shorten URL');
          }
        })
        .then(data => {
          this.shortenedUrl = data;
          this.error = '';
        })
        .catch(error => {
          this.error = 'Error: ' + error.message;
          this.shortenedUrl = '';
        });
    }
  }
};
</script>

<style scoped>
.shorten-url-form {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.form {
  display: flex;
  flex-direction: column;
}

.input-field {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

.submit-button {
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.submit-button:hover {
  background-color: #0056b3;
}

.shortened-url {
  margin-top: 10px;
  font-size: 18px;
  color: #007bff;
}
.margin-top-20 {
   margin-top: 20px;
}
.error-message {
  margin-top: 10px;
  font-size: 16px;
  color: #dc3545;
}
</style>