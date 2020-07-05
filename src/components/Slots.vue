<template>
<div>
    <h1>{{title}}</h1>
    <slot name='first'>Deafult 1</slot>
    <slot name='second'>Deafult 2</slot>
    
</div>
</template>

<script>
export default {
    props: ['title']
}
</script>