<template>
    <button @click="$emit('btnClick')" class="btn red darken-1">{{ text }}</button>
</template>
<script>
export default {
    name:'Button-file',
    props:{
        text: String,
    }
}
</script>