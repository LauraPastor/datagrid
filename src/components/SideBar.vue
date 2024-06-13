<template>
    <v-navigation-drawer expand-on-hover rail>
      <v-list>
        <!-- TODO: Replace with your actual logo and details -->
        <v-list-item prepend-avatar="https://picsum.photos/seed/picsum/400/400" subtitle="htw-berlin@htw.de"
          title="HTW Berlin"></v-list-item>
      </v-list>
  
      <v-divider></v-divider>
  
      <v-list density="compact" nav>
        <v-list-item prepend-icon="mdi-image" title="Color Gallery" @click="selectColorGallery"></v-list-item>
        <v-list-item prepend-icon="mdi-dialpad" title="Grayscale Gallery" @click="selectGrayscaleGallery"></v-list-item>
      </v-list>
    </v-navigation-drawer>
  </template>
  
  <script>
  import { defineEmits } from 'vue';
  
  export default {
    name: 'SideBar',
    emits: defineEmits(['selectOption']),
    setup(props, { emit }) {
      const selectColorGallery = () => {
        emit('selectOption', true); // Emitting 'selectOption' event with true (isColor=true)
      };
  
      const selectGrayscaleGallery = () => {
        emit('selectOption', false); // Emitting 'selectOption' event with false (isColor=false)
      };
  
      return {
        selectColorGallery,
        selectGrayscaleGallery
      };
    }
  };
  </script>
  
