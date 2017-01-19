<template>
  <div id="main">
    <h1>{{ title }}</h1>

    <input type="text" class="input_todo"
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
</template>

<script>

export default {
  name: 'index',
  data () {
    return {
        title: 'Hello Vue!',
        items: [],
        new_item: ''
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
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
