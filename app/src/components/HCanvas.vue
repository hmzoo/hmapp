<template>
    <canvas ref="canvas" :width="width" :height="height" @mousedown="handleMouseDown" @mousemove="handleMouseMove" @mouseup="handleMouseUp"></canvas>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const props = defineProps({
    width: {
        type: Number,
        default: 500
    },
    height: {
        type: Number,
        default: 500
    }
});

const canvas = ref(null);
const isDragging = ref(false);
const dragIndex = ref(null);
const points = ref([
    { x: 50, y: 50 },
    { x: 150, y: 50 },
    { x: 250, y: 50 },
    { x: 350, y: 50 },
    { x: 50, y: 150 },
    { x: 150, y: 150 },
    { x: 250, y: 150 },
    { x: 350, y: 150 }
]);

const handleMouseDown = (event) => {
    const { x, y } = getMousePos(event);
    const index = points.value.findIndex(point => isPointInCircle(point, x, y));
    if (index !== -1) {
        isDragging.value = true;
        dragIndex.value = index;
    }
};

const handleMouseMove = (event) => {
    if (isDragging.value) {
        const { x, y } = getMousePos(event);
        points.value[dragIndex.value] = { x, y };
        redraw();
    }
};

const handleMouseUp = () => {
    isDragging.value = false;
    dragIndex.value = null;
};

const getMousePos = (event) => {
    const rect = canvas.value.getBoundingClientRect();
    return {
        x: event.clientX - rect.left,
        y: event.clientY - rect.top
    };
};

const isPointInCircle = (point, x, y) => {
    const dx = point.x - x;
    const dy = point.y - y;
    return Math.sqrt(dx * dx + dy * dy) < 5;
};

const redraw = () => {
    const context = canvas.value.getContext('2d');
    context.clearRect(0, 0, props.width, props.height);
    context.fillStyle = 'lightgray';
    context.fillRect(0, 0, props.width, props.height);

    context.fillStyle = 'black';
    points.value.forEach(point => {
        context.beginPath();
        context.arc(point.x, point.y, 5, 0, Math.PI * 2);
        context.fill();
    });
};

onMounted(() => {
    const context = canvas.value.getContext('2d');
    context.fillStyle = 'lightgray';
    context.fillRect(0, 0, props.width, props.height);
    redraw();
});
</script>

<style scoped>
canvas {
    border: 1px solid #000;
}
</style>
