<template>
  <div id="app">
    <header class="header">
      <div class="header__section container">
        <div class="header__section__title-section">
          <h1 class="header__section__title-section__heading">TODO APP</h1>
          <p class="header__section__title-section__heading-text">
            Create your list of tasks, and make your life easier
          </p>
        </div>
        <img
          src="../src/assets/star-logo.png"
          alt="TODO logo of the app"
          class="header__section__logo-image"
        />
      </div>
      <main class="main">
        <div class="main__section container">
            <div class="main__section__card">
                <div class="main__section__card__details">
                    <h3 class="main__section__card__details__card-heading">List of your tasks</h3>
                </div>
                <form class="main__section__card__card-input">
                    <input v-model="task" type="text" placeholder="Add task" name="content" class="main__section__card__card-input__input-section">
                    <button @click.prevent="saveLocalTodo" class="main__section__card__card-input__input-button">Add</button>
                </form>
                <div class="main__section__card__card-main">
                    <ul class="main__section__card__card-main__todo-list">
                      <div v-for="(task, index) in tasks" :key="index" class="main__section__card__card-main__todo-list__task-item">
                        <input @click="updateToDo(index)" :checked="task.done === true" class="main__section__card__card-main__todo-list__task__checkBox-input" type="checkbox">
                        <li :class="(task.done === true) ? 'completed' : ''" class="main__section__card__card-main__todo-list__task-item__name">{{task.name}}</li>
                        <button @click="removeLocalTodo(index)" class="main__section__card__card-main__todo-list__task__button-remove">remove</button>
                      </div>
                    </ul>
                </div>
            </div>
        </div>
    </main>
    </header>
  </div>
</template>
<script>

export default {

  name: "app",

  data() {
    return {
      task: "",
      tasks: []
    }
  },
  created () {
    this.tasks = JSON.parse(localStorage.getItem('tasks')) || [];
  },
  methods: {
    saveLocalTodo() {
      this.tasks.push({
        name: this.task,
        done: false
      });
      this.task = "";
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    removeLocalTodo(index) {
      this.tasks.splice(index, 1);
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    updateToDo(index) {
      const todo = this.tasks[index];
      if(todo.done === false) {
        todo.done = true;
      } else {
        todo.done = false;
      }
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }
  }
}


</script>
<style src="./css/style.css" />
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

.header__section {
  background-image: linear-gradient(to top right, #cce0ff, #8a2eff);
  border-radius: 130px;
}

.header__section__title-section__heading {
  font-size: 80px;
  letter-spacing: 5px;
  color: #fff;
}

.header__section__title-section__heading-text {
  font-size: 25px;
  letter-spacing: -0.5px;
  color: #fff;
}

.header__section__logo-image {
  display: block;
  width: 70px;
  margin: 5px auto 0 auto;
  padding-bottom: 10px;
}

//MAIN
.main__section{
    background-color: #B49FFF;
    border-radius: 130px;
    height: 50vh;
    
}

.main__section__card{
    width: 70%;
    height: 70%;
    padding: 20px 0;
    margin: 0 auto;
    font-family: 'Quicksand', sans-serif;
}

.main__section__card__details__card-heading{
    text-align: center;
    font-size: 30px;
    color: #fff;
}

.main__section__card__card-main{

    height: 100%;
    background-color: #fff;
    padding: 15px;
    border-radius: 30px;
}

.main__section__card__card-input{
    margin-top: 10px;
    display: flex;
    justify-content: center;
    gap: 10px;
}

.main__section__card__card-input__input-section {
    font-size: 20px;
    font-family: 'Quicksand', sans-serif;
    font-weight: 500;
    border-radius: 5px;
    border: none;
    padding: 0 10px;
}

.main__section__card__card-input__input-button{
    font-family: 'Quicksand', sans-serif;
    font-size: 20px;
    font-weight: 600;
    color: #B49FFF;
    background-color: #fff;
    border: none;
    padding: 0 15px;
    border-radius: 5px;
}

.main__section__card__card-main{
    
    width: 100%;
    margin-top: 20px;
    overflow: auto;
}

.container {
    max-width: 60rem;
    margin: 35px auto 0 auto;
  }

.main__section__card__card-main__todo-list {
    
    list-style: none;
    
}

.main__section__card__card-main__todo-list__task-item {

    background-color: none;
    font-family: 'Quicksand', sans-serif;
    margin: 0.5rem;
    font-size: 1.5rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;

}

.main__section__card__card-main__todo-list__task__checkBox-input, .main__section__card__card-main__todo-list__task__button-remove {

    padding: 0.2rem;
}

.completed {

    text-decoration: line-through;
    opacity: 0.5;
}

.main__section__card__card-main__todo-list__task__button-remove {
    font-family: 'Quicksand', sans-serif;
}

.main__section__card__card-main__todo-list__task-item__inside{
    display: flex;
    
    width: 100%;
}

.main__section__card__card-main__todo-list__task-item__name{
    font-size: 18px;
    font-weight: 500;
}

.main__section__card__card-main__todo-list__task__button-remove{
    border: none;
    font-size: 18px;
    font-weight: 600;
    text-transform: uppercase;
    color: #fff;
    background-color: #A26FFF;
    border-radius: 8px;
    padding: 0 10px;
}

[type="checkbox"] {
    opacity: 1;
    position: relative;
    width: 30px;
    height: 30px;
    
}

[type="checkbox"]::before {
    content: "";
    position: absolute;
    width: 25px;
    height: 25px;
    outline: 2px solid #A26FFF;
    background-color: #fff;
    z-index: 1;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    
}

[type="checkbox"]:checked::before{
    content: "";
    position: absolute;
    width: 25px;
    height: 25px;
    outline: 2px solid green;
    background-color: #fff;
    z-index: 1;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

[type="checkbox"]:checked::after{
    content: "";
    position: absolute;
    width: 25px;
    height: 25px;
    z-index: 1;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-image:url(/src/assets/checkjpg.jpg);
    background-size: contain;
    
}
</style>
