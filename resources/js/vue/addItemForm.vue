<template>
        <div class="row inputBox">
                <input type="text" class="form-control inputText" placeholder="What do you need to do today?" v-model="item.name">
                <button type="submit" class="btn btn-primary" :disabled="item.name ? false : true" @click="addItem()" >Add</button>
        </div>

</template>

<script>
export default {
    data: function(){
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem(){
            if(this.item.name == ''){
                return;
            } else {
                axios.post('api/item/store', {
                    item: this.item
                })
                .then( response => {
                    if( response = 201 ){
                        this.item.name = "";
                         this.$emit('reloadlist');
                    }
                })
                .cacth(error => {
                    console.log(error);
                })
            }
        }
    }
}
</script>

<style scoped>
.inputBox {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
}
.inputText{
    width: 80%;
    margin-right: 10px;
}
</style>
