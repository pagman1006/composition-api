<template>
    <div>
        <h1>Counter View</h1>
        <h2>{{ counter }}</h2>

        <button @click="increase">+1</button>
        <button @click="decrease">-1</button>
    </div>
</template>

<script>
import useCounter from '@/composables/useCounter'

export default {
    name: 'Counter',
    props: {},
    emits: [],
    setup() {
        const { counter, decrease, increase } = useCounter(25)

        return {
            counter,
            decrease,
            increase
        }
    }
}
</script>

<style lang="scss" scoped></style>