<template>
  <v-card class="my-4 mx-lg-auto" width="350px">
    <v-file-input
      v-model="file"
      :rules="rules"
      accept=".aasx"
      label="Data file"
      placeholder="Data file"
      prepend-icon="mdi-paperclip"
      @change="validateFile"
    ></v-file-input>
    <v-alert v-if="error" type="error" dismissible class="mt-2">
      {{ error }}
    </v-alert>
    <v-alert v-if="message" :type="alertType" dismissible class="mt-2">
      {{ message }}
    </v-alert>
    <div v-if="file">
      <p>{{ file.name }}</p>
    </div>
  </v-card>
</template>

<script>
import axios from 'axios';

export default {
  data: () => ({
    file: null,
    error: null,
    message: null,
    alertType: 'success',
    rules: [
      value => {
        if (!value) return 'Data file is required.';
        if (value.size >= 2000000) return 'Data file should be less than 2 MB!';
        return true;
      }
    ]
  }),
  methods: {
    validateFile() {
      this.error = null;
      if (this.file && this.file.name.split('.').pop().toLowerCase() !== 'aasx') {
        this.error = 'Only .aasx files are accepted!';
        this.file = null; // Reset the file
      }
    },
    async uploadFile() {
      if (!this.file) {
        this.error = 'Please select a file';
        return;
      }

      const formData = new FormData();
      formData.append('myFile', this.file);

      try {
        const response = await axios.post('http://localhost:3000/upload', formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        });
        this.message = response.data.message;
        this.alertType = 'success';
      } catch (error) {
        this.message = error.response?.data?.message || 'File upload failed';
        this.alertType = 'error';
      }
    }
  }
}
</script>

<style scoped>
/* Add any styles specific to this component here */
</style>
