<script setup>

const props = defineProps({
    message: String
})

const emit = defineEmits(['tomato'])
const sendResponse = () => {
    emit("tomato", "子コンポーネントからの返答")
}
</script>

<template>
    <div>
        <h2>子コンポーネン</h2>
        <p>親からのメッセージ: {{ message }}</p>

        <button @click="sendResponse">親にデータを送る</button>
    </div>
</template>