<script setup>
import { createClient } from '@supabase/supabase-js'
import { data } from 'autoprefixer'
import { onMounted } from 'vue'
import PhotoCard from './PhotoCard.vue';

const supabaseUrl = 'https://lsrxwmlpvsctgsllqejr.supabase.co'
// const supabaseKey = TODO: store this in a GH secret
const supabaseClient = createClient(supabaseUrl, supabaseKey)

const photos = ref([])

onMounted(async () => {
    const { data, error } = supabaseClient.storage.from('sports').list()
    if (error) {
        console.error(error)
        return
    }

    sports.value = data
        .filter(file => file.name.match(/\.(jpg|jpeg|png|gif)$/i))
        .map(file => ({
            id: file.id || file.name,
            image: supabase.storage.from('photos').getPublicUrl(file.name).data.publicUrl,
            title: file.name,
            description: ''
        }))
})

</script>

<template>
    <div class="gallery columns-2 gap-4">
        <PhotoCard 
            v-for="photo in photos" 
            :key="photo.id" 
            :image="photo.image" 
            :title="photo.title"
            :description="photo.description" 
        />
    </div>
</template>

<style scoped></style>