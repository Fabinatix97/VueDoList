<template>
  <section class="todo-list">
                
      <h3>To-do List</h3>
      
      <div class="all-todos" v-if="items">
          <div>
              <p>ToDo 1</p>
          </div>
      </div>

      <button v-if="items.length" class="clear" @click="items=[]">Clear All</button>

      <input type="text" placeholder="Add new to-do" v-model="newItem.text">
      <button class="add" @click="addItem()">Add</button>

      <div class="instructions">
          Instructions:
          <ul>
              <li>Click the to-do text to toggle between done / undone</li>
              <li>Use clear all button to remove all items</li>
              <li>Use the input field to add new to-dos</li>
          </ul>
      </div>
  </section>
</template>

<script>

export default {
  name: 'App',

  data() {
    return {
        items: [],
        newItem: {
          crossed: false
        }
    }
  },

  methods: {
    addItem: function() {
      if(this.newItem.text) {
          this.items.push(this.newItem);
          this.newItem = {
              crossed: false
          };
          localStorage.setItem("items", JSON.stringify(this.items));
      } else {
          alert("Field must be filled")
      }
    }
  }
}

</script>

<style lang="scss">
#app {
  margin: 0;
  font-family: 'Open Sans', sans-serif;
  display: flex;
  justify-content: center;
  align-items:flex-start;
  flex-wrap: wrap;
  padding-top: 60px;

  .todo-list {
    flex-wrap: wrap;
    border: 1px solid lightgrey;
    background-color: rgb(248, 248, 248);
    padding: 20px;
    max-width: 500px;
    min-width: 300px;
    text-align: center;
    border-radius: .25rem;

    input {
      box-sizing: border-box;
      height: 28px;
      border-radius: .25rem;
      width: 80%;
      border: 1px solid lightgrey;
      margin-top: 32px;
    }

    h3 {
      text-align: center;
      margin-top: 24px;
      width: 100%;
    }

    button.clear {
      margin-top: 24px;
    }
  }

  button {
    background-color: transparent;
    cursor: pointer;
    box-sizing: border-box;
    height: 28px;
    border-radius: .25rem;
    color: #fff;

    &:hover {
    opacity: 0.8;
    }

    &.add {
    background-color: #007bff;
    border: 1px solid  #007bff;
    margin-left: 2px;
    }

    &.clear {
    background-color: #dc3545;
    border: 1px solid #dc3545;
    display: block;
    margin: auto;
    }

    &:focus {
    outline:0;
    }
  }

  .all-todos .single-todo {
    display: flex;
    align-items: center;
    justify-content: center;

    p {
      margin: 12px 0;
      cursor: pointer;
    }

    &.done p {
      text-decoration: line-through;
    }

    button.remove {
      width: 12px;
      height: 12px;
      border: none;
      /*background: transparent url('img/remove.png') no-repeat center;*/
      background-size: contain;
      cursor: pointer;
      margin-left: 8px;
    }

    button.clear {
      margin-top: 24px;
    }
  }

  div.instructions {
    font-size: 11px;
    margin-top: 40px;
    color: grey;

    ul {
      list-style: inside;
      text-align: center;
      padding: 0;

      li {
        margin: 4px auto;
      }
    }
  }
}
</style>
