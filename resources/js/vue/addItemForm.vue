<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <button @click="addItem()" class="submit">Add</button>
    </div>
</template>
<script>
export default{
    data: function(){
        return{
            item:{
                name: ''
            }
        }
    },
    methods: {
        addItem(){
            if(this.item.name == ''){
                return;
            }
            axios.post('api/item/store', {
                item: this.item
            }).then(response=>{
                if(response.status == 201){
                    this.item.name = '';
                    this.$emit('reloadlist')
                }
            }).catch(error=>{
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
.addItem{
    display: flex;
    justify-content: center;
    align-items: center;
}

input{
    background: #f7f7f7;
    border-radius: 50px;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}

.submit{
    width: 25%;
}
</style>