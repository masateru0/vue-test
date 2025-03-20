<script setup>
import { ref, reactive, computed, watch, watchEffect, onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from "vue";
import yadonUrl from "@/assets/yadon.jpg";
import yadokingUrl from "@/assets/yadoking.jpg"
import ChildComponent from "./components/ChildComponent.vue";

const imgUrl = ref(yadonUrl)
const status = ref('kakaka')
const isVisible = ref(true)
const fruits = ref(['Apple', 'Grape', 'Banana'])
const message = ref('')
const isActive = ref(true)
const textColor = ref('blue')
const fontSize = ref(16)
const price = ref(100)
const quantity = ref(2)
const count = ref(0)
const parentMessage = ref('親コンポーネントのメッセージ')
const childResponse = ref('')
const counts = ref(0)

const changeImage = () => {
    imgUrl.value = imgUrl.value === yadonUrl ? yadokingUrl : yadonUrl
}

const changeStyle = () => {
    textColor.value = textColor.value === 'blue' ? 'red' : 'blue'
    fontSize.value = fontSize.value === 16 ? 24 : 16
}

const totalPrice = computed(() => price.value * quantity.value)

// watch(count, (newVal, oldVal) => {
//     console.log(`Count changed from ${oldVal} to ${newVal}`);
// })

watchEffect(() => {
    console.log(`Count is now: ${count.value}`);
})

const handleChildEvent = (banana) => {
    childResponse.value = banana
}

const increment =() => {
    counts.value++
}

onBeforeMount(() => {
    console.log("onBeforeMount: DOMにマウントされる直前");
})

onMounted(() => {
    console.log("onMounted: DOMに描画された（イベントリスナー追加などに最適）");
})

onBeforeUpdate(() => {
    console.log(`onBeforeUpdate: データ変更前（旧データ: ${counts.value}）`);
})

onUpdated(() => {
    console.log(`onUpdated: データ変更後（新データ: ${counts.value}）`);
})

onBeforeUnmount(() => {
    console.log("onBeforeUnmount: コンポーネントが削除される直前");
})

onUnmounted(() => {
    console.log("onUnmounted: コンポーネントが削除された後（クリーンアップ）");
})


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

    <div>
        <p>価格: {{ price }} 円</p>
        <p>数量: {{ quantity }}</p>
        <p>合計: {{ totalPrice }} 円</p>

        <button @click="quantity++">数量を増やす</button>
    </div>

    <div>
        <p>カウント: {{ count }}</p>
        <button @click="count++">増やす</button>
    </div>

    <div>
        <h1>親コンポーネント</h1>
        <p>子に渡すメッセージ: {{ parentMessage }}</p>
        <ChildComponent :message="parentMessage" @tomato="handleChildEvent"/>

        <p>子からのメッセージ: {{ childResponse }}</p>
    </div>

    <div>
        <h2>カウント: {{ counts }}</h2>
        <button @click="increment">カウントアップ</button>
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
