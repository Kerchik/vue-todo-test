<template>
    <div>
        <ul>
            <li v-for="(item) in array" v-bind:key='item'>
                {{item}}
            </li>
        </ul>
        <button @click='createElem'>Create new element</button>
    </div>
</template>

<script>
export default {
    props: ['array'],
    methods: {
        createElem() {
            this.$emit('create-element')
        }
    }
}
</script>