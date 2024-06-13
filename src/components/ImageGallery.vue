<template>
    <v-row class="pt-6 ">
        <v-col v-for="n in 200" :key="n" cols="4" sm="3">
            <v-card :elevation="isHovering ? 12 : 2" v-bind="props" @click="copyUrl(`https://picsum.photos/500/300?random=${n * 5 + 10}${p.isWithColor ? '' : '&grayscale'}`)">
                <v-img :src="`https://picsum.photos/500/300?random=${n * 5 + 10}${p.isWithColor ? '' : '&grayscale'}`" aspect-ratio="1" cover
                    :lazy-src="`https://picsum.photos/10/6?random=${n * 5 + 10}${p.isWithColor ? '' : '&grayscale'}`">
                    <template v-slot:placeholder>
                        <v-row class="fill-height ma-0" align="center" justify="center">
                            <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                        </v-row>
                    </template>
                </v-img>
            </v-card>
        </v-col>
    </v-row>
</template>

<script setup>
import {defineProps} from 'vue'

const p = defineProps(['isWithColor'])
const copyUrl = async (url) =>    {
    await navigator.clipboard.writeText(url)
    .then(() => {
        console.log('URL copied to clipboard')
    })
    .catch((error) => {
        console.error('Failed to copy: ', error)
    })
}
</script>
