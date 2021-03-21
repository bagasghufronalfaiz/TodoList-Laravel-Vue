<template>
    <div class="container-sm bg-light height">
        <div class="row">
            <div class="col-12 header">
                <h2>To Do List</h2>
            </div>
            <div class="col-12">
                <add-item-form v-on:reloadlist="getList()"/>
            </div>
            <div class="col-12">
                <list-view :items="items" v-on:reloadlist="getList()"/>
            </div>
        </div>
    </div>
</template>

<script>
import addItemForm from './addItemForm'
import listView from './listView'

export default {
    components:{ addItemForm, listView },
    data: function(){
        return {
            items: []
        }
    },
    methods:{
        getList(){
            axios.get('/api/items')
            .then(response => {
                this.items = response.data
            })
            .cacth(error => {
                console.log(error);
            })
        }
    },
    created(){
        this.getList();
    }
}
</script>

<style scoped>
.header {
    text-align: center;
    padding: 20px;
    font-weight: 700;
}
.height{
    min-height: 100vh;
}
</style>
