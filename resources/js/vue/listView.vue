<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item :item="item" class="item" v-on:itemchanged="$emit('reloadlist')" />
        </div>
    </div>
</template>

<script>
import listItem from './listItem.vue'

export default{
    props: ['items'],
    components: {
        listItem
    }
}
</script>

<style>
.item{
    border-radius: 25px;
    background: #e6e6e6;
    padding: 5px;
    margin: 5px;
}
</style>