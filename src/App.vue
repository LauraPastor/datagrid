<template>
  <v-app>

    <SideBar @selectOption="onSelectOption" />
    <v-main>
      <v-card class="pa-md-4 mx-lg-auto" width="500px">
        <UploadInput />
        <GridData />
      </v-card>
      <v-card class="my-5 px-5">
        <ImageGallery :isWithColor="isWithColor" />
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
import { ref } from 'vue'
import SideBar from './components/SideBar.vue'
import UploadInput from './components/UploadInput.vue'
import GridData from './components/GridData.vue'
import ImageGallery from './components/ImageGallery.vue'

export default {
  name: 'App',
  components: {
    SideBar,
    UploadInput,
    GridData,
    ImageGallery
  },
  setup() {
    const isWithColor = ref(true);

    const onSelectOption = (isColor) => {
      isWithColor.value = isColor;
    };

    return {
      isWithColor,
      onSelectOption
    };
  }
}
</script>