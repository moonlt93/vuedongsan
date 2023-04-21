<template>
<div>
    <img class="room-img" :src="items.image"/>
    <h4 @click="$emit('openModal',items.id)">{{ items.title }}</h4>
    <p>{{ items.price }}원</p>
</div>
</template>
<script>

export default {
    name:'Card',
    props :{
        items: Object,
    } 
}
</script>
<style>
    
</style>