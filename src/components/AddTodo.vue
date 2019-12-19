<template>
  <div>
      <form @submit.prevent="addTodo">
          <input type="text" v-model="title" name="title" placeholder="Add todo...">
          <input type="submit" value="Submit" class="btn">
      </form>
  </div>
</template>
<script>
//import uuid from 'uuid';

export default {
    name: "AddTodo",
    data(){
        return{
            title: ''
        }
    },
    methods: {
        addTodo() {
            /* PREVENT FORM RELOAD */
            //e.preventDefault();
            //e.stopPropagation();
            //e.stopImmediatePropagation();
            const newTodo = {
                //id: uuid.v4(), NOW WE USE AN API THAT PROVIDES AN ID, WE DON'T NEED TO GENERATE ONE HERE
                title: this.title,
                completed: false
            }
            console.log(newTodo);
            //Send up to parent
            this.$emit('add-todo', newTodo);

            this.title = '';
        }
    }
}
</script>
<style scoped>
    form{
        display: text;
    }
    input[type="text"]{
        flex: 10;
        padding: 5px
    }
    input[type="submit"]{
        flex: 2;
    }
</style>