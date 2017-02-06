<template>
    <div id="main" class="container">
        <div class="row">
            <div class="col-md-8 col-sm-12 col-md-offset-2">
                <div class="row">
                    <input type="text" class="input_todo col-md-12 form-control input-lg"  placeholder="Input something"
                                v-model="new_item"
                                v-on:keyup.enter="addNew()">
                </div>

                <div class="row">
                    <ul class="list-group">
                    <!-- v-for 还支持一个可选的第二个参数为当前项的索引 -->
                        <li class="list-group-item"
                            v-for="(item, index) in items"
                            v-bind:class="{finished: item.is_finished}">
                             <input type="checkbox" 
                                    @click="toggleFinish(item)">
                            {{ item.label }}
                            <button class="destroy btn btn-danger btn-sm"
                                @click="removeTodo(index)">X</button>
                        </li>
                    </ul>
                </div>
                
            </div>
        </div>
    </div>

</template>

<script>

import Storage from '../assets/js/storage.js'

export default {
    name: 'index',
    data () {
        return {
            title: 'TodoList Vuejs 2.0',
            items: Storage.fetch(),
            new_item: ''
        }
    },
    watch: {
        items: {
            handler: function (item) {
                Storage.save(item)
            },
            deep: true
        }
    },
    methods: {

        toggleFinish: function (item) {
            item.is_finished = !item.is_finished
        },
        addNew: function () {
            this.items.push({
                label: this.new_item,
                is_finished: false
            })
            this.new_item = ''
        },
        removeTodo: function(index) {
            this.items.splice(index, 1)
        }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.finished {
    text-decoration: line-through
}

</style>
s