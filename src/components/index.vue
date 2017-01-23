<template>
    <div id="main" class="row">
        <div class="col-md-8 col-sm-12 col-md-offset-2">
                    
            <input type="text" class="input_todo col-md-12"
                v-model="new_item"
                v-on:keyup.enter="addNew()">
            
            <ul>
                <li v-for="item in items"
                    v-bind:class="{finished: item.is_finished}"
                    @click="toggleFinish(item)">
                    {{ item.label }}
                </li>
            </ul>
            
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
