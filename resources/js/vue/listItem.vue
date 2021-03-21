<template>
    <div>
        <div class="custom-control custom-checkbox item">
            <input type="checkbox" class="custom-control-input" :id="[item.id]" @change="updateCheck()" v-model="item.completed" />
            <label class="custom-control-label" :for="[item.id]" :class="[item.completed ? 'completed' : '' , 'itemText']">
            {{item.name}}
            </label>
            <button type="submit" class="btn btn-danger btn-sm" @click="removeItem()">Remove</button>
        </div>
    </div>
</template>

<script>
export default {
    props:['item'],
    methods:{
        updateCheck(){
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then( response => {
                if( response.status = 200) {
                    this.$emit('itemchange');
                }
            })
            .catch(error => {
                console.log(error);
            })
        },
        removeItem(){
            axios.delete('api/item/' + this.item.id, {
                item: this.item
            })
            .then( response => {
                if( response.status = 200) {
                    this.$emit('itemchange');
                }
            })
            .catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
.completed {
    text-decoration: line-through;
    color: #999999;
}
.itemText {
    width: 100%;
    margin-left: 20px;
}
.item{
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px 0px;
}
</style>
