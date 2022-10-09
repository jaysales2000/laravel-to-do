<template>
    <div id="bg">
        <div class="main">
            <div class="todoListContainer">
                <div class="heading">
                    <div class="title">
                        Todo List
                    </div>
                    <div class="team">
                        Team JOHTO
                    </div>
                    <br>
                    <add-item-form v-on:reloadlist="getList() " />
                </div>


                <list-view :items="items" v-on:reloadlist="getList() " />
            </div>
        </div>


    </div>
</template>

<script>
import addItemForm from './addItemForm.vue'
import listView from './listView.vue'
export default {
    components: {
        addItemForm,
        listView
    },
    data: function () {
        return {
            items: []
        }
    },
    methods: {
        getList() {
            axios.get('api/items')
                .then(response => {
                    this.items = response.data
                })
                .catch(error => {
                    console.log(error);
                })
        }
    },

    created() {
        this.getList()
    }
}
</script>

<style scoped>
.todoListContainer {
    width: 350px;
    margin: auto;
    padding: 5%;
}

.heading {
    border-radius: 25px;
    background: #e6e6e6;
    padding: 10px;
}

.title {
    font-weight: bold;
    font-size: 35px;
}

.main {
    width: 30%;
    height: 1000px;
    margin: auto;
    font-family: monospace;
}

#bg {
    background-image: url('https://wallpapercave.com/wp/wp2665743.jpg');
    background-repeat: no-repeat;
    background-size: cover;

}
</style>