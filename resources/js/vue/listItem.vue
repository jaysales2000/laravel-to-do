<template>
    <div class="item">
        <input type="checkbox" @change="updateCheck()" v-model="item.completed"/>
        <span :class="[item.completed ? 'completed' : '', 'itemText']">{{item.name}}</span>
        <button @click="removeItem()" class="trashcan">X</button>
    </div>
</template>
<script>
import axios from 'axios';

export default{
    props: ['item'],
    methods:{
        updateCheck(){
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then(response=>{
                if(response.status == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch(error=>{
                console.log(error);
            })
        },
        removeItem(){
            axios.delete('api/item/' + this.item.id)
            .then(response=>{
                if(response.status == 200){
                    this.$emit('itemchanged');
                }
            })
            .catch(error=>{
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
.completed{
    text-decoration: line-through;
    color: grey;
}

.itemText{
    width: 100%;
    margin-left: 20px;
    font-size: 20px;
}

.item{
    display: flex;
    justify-content: center;
    align-items: center;
}

.trashcan{
    background-color: red;
    color: white;
}

button{
    border-radius: 25px;

}
</style>