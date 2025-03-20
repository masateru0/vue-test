<script setup>
import { ref, reactive } from "vue";
import yadonUrl from "@/assets/yadon.jpg";
import yadokingUrl from "@/assets/yadoking.jpg"

const imgUrl = ref(yadonUrl)
const status = ref('kakaka')
const isVisible = ref(true)
const fruits = ref(['Apple', 'Grape', 'Banana'])
const message = ref('')
const isActive = ref(true)
const textColor = ref('blue')
const fontSize = ref(16)

const changeImage = () => {
    imgUrl.value = imgUrl.value === yadonUrl ? yadokingUrl : yadonUrl
}

const changeStyle = () => {
    textColor.value = textColor.value === 'blue' ? 'red' : 'blue'
    fontSize.value = fontSize.value === 16 ? 24 : 16
}

</script>

<template>
    <div>
        <img :src="imgUrl" alt="yadon">
        <button @click="changeImage">change!</button>

        <p v-if="status === 'loading'">Loading...</p>
        <p v-else-if="status === 'error'">Error!!</p>
        <p v-else>Success!</p>

        <p v-show="isVisible">This is Visible</p>
        <button @click="isVisible = !isVisible">toggle</button>

        <ul>
            <li v-for="(fruit, index) in fruits" :key="index">
                {{ index }} : {{ fruit }}
            </li>
        </ul>

        <input v-model="message" placeholder="なんか書けや。。。">
        <p>Message: {{ message }}</p>

        <p :class="{ active: isActive, inactive: !isActive }">This is a message</p>
        <button @click="isActive = !isActive">Toggle class</button>

        <p :style="{ color: textColor, fontSize: fontSize + 'px' }">Styled text</p>
        <button @click="changeStyle">Change Style</button>
    </div>
</template>

<style scoped>
    img {
        width: 600px;
        height: 600px;
    }

    .active {
        color: green;
        font-weight: bold;
    }

    .inactive {
        color: gray;
    }
</style>
