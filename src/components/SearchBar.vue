<template>
  <div>
    <input @keydown.enter="onInput" type="text" />
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  methods: {
    onInput: function (event) {
      // This event will inform App.vue that an input happened. We can name our own events. This line emits an event called 'TermChange' and
      // passes in the value of the input (whatever the user entered). We can use that input value when receiving this event in App.vue
      // Note how it is possible to call the input (event.target.value) whatever we want in the method that gets called when this event is fired.
      // In this case, we called it 'searchTerm' in App.vue
      this.$emit('TermChange', event.target.value);
    },
  },
};
</script>

<style scoped>
input {
  width: 75%;
}

div {
  text-align: center;
  margin: 20px;
}
</style>
