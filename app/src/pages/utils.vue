<template>
    <div class="h-camera">
        <video ref="video" autoplay></video>
        <button @click="capturePhoto">Capture Photo</button>
        <canvas ref="canvas" style="display: none;"></canvas>
    </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const video = ref(null);
const canvas = ref(null);
const videoStream = ref(null);

const startCamera = async () => {
    try {
        videoStream.value = await navigator.mediaDevices.getUserMedia({ video: true });
        video.value.srcObject = videoStream.value;
    } catch (error) {
        console.error('Error accessing camera: ', error);
    }
};

const capturePhoto = () => {
    const canvasElement = canvas.value;
    const videoElement = video.value;
    canvasElement.width = videoElement.videoWidth;
    canvasElement.height = videoElement.videoHeight;
    const context = canvasElement.getContext('2d');
    context.drawImage(videoElement, 0, 0, canvasElement.width, canvasElement.height);
    const photo = canvasElement.toDataURL('image/png');
    emit('photo-captured', photo);
};

onMounted(() => {
    startCamera();
});

onBeforeUnmount(() => {
    if (videoStream.value) {
        videoStream.value.getTracks().forEach(track => track.stop());
    }
});
</script>

<style scoped>
.h-camera {
    display: flex;
    flex-direction: column;
    align-items: center;
}
video {
    width: 100%;
    max-width: 600px;
}
button {
    margin-top: 10px;
}
</style>
