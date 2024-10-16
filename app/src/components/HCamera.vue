<template>
    <div>
        <canvas ref="canvas"></canvas>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const canvas = ref(null);

onMounted(() => {
    const video = document.createElement('video');
    video.autoplay = true;

    navigator.mediaDevices.getUserMedia({ video: true })
        .then(stream => {
            video.srcObject = stream;
            const ctx = canvas.value.getContext('2d');

            const draw = () => {
                ctx.drawImage(video, 0, 0, canvas.value.width, canvas.value.height);
                requestAnimationFrame(draw);
            };

            video.addEventListener('loadedmetadata', () => {
                canvas.value.width = video.videoWidth;
                canvas.value.height = video.videoHeight;
                draw();
            });
        })
        .catch(err => {
            console.error('Error accessing the camera: ', err);
        });
});
</script>

<style scoped>
canvas {
    width: 100%;
    height: auto;
}
</style>