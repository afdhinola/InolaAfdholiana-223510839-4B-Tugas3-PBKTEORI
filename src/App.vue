<template>
  <div>
    <header>
      <nav>
        <ul>
          <li><button @click="activeTab = 'todos'">Todos</button></li>
          <li><button @click="activeTab = 'posts'">Post</button></li>
        </ul>
      </nav>
    </header>

    <main id="content">
      <div v-if="activeTab === 'todos'">
        <TodoList />
      </div>
      <div v-else-if="activeTab === 'posts'">
        <Post />
      </div>
    </main>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';
import Post from './components/Post.vue';

export default {
  data() {
    return {
      activeTab: 'todos'
    };
  },
  components: {
    TodoList,
    Post
  }
}
</script>

<style>
body {
  font-family: cursive;
  background-color: #A3966A;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

header {
  background-color: #482E1D;
  padding: 10px;
  width: 100%;
  display: flex;
  justify-content: center;
  border-radius: 15px;
}

nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
}

nav li {
  margin: 0 10px;
}

nav button {
  background-color: #F0DAAE;
  color: #482E1D;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-family: cursive;
  border-radius: 15px;
}

nav button:hover {
  background-color: #90553C;
  color: #F0DAAE;
}

main {
  width: 100%;
  width: 600px;
  padding: 20px;
  border-radius: 10px;
  font-family:cursive;
}
</style>
