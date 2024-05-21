<template>
    <div v-if="activeTab === 'posts'">
      <h2>User Posts</h2>
      <div class="post-component">
        <select v-model="selectedUser" @change="fetchUserPosts">
          <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
        </select>
        <div class="post-container">
          <div v-if="selectedUser !== null" v-for="post in userPosts" :key="post.id" class="post">
            <h3>{{ post.title }}</h3>
            <p>{{ post.body }}</p>
          </div>
          <div v-if="selectedUser !== null && userPosts.length === 0" class="no-posts">
            No posts available for selected user.
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        activeTab: 'posts',
        users: [],
        selectedUser: null,
        userPosts: []
      };
    },
    methods: {
      fetchUsers() {
        fetch('https://jsonplaceholder.typicode.com/users')
          .then(response => response.json())
          .then(data => {
            this.users = data;
          });
      },
      fetchUserPosts() {
        if (this.selectedUser !== null) {
          fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUser}`)
            .then(response => response.json())
            .then(data => {
              this.userPosts = data;
            });
        } else {
          this.userPosts = [];
        }
      }
    },
    created() {
      this.fetchUsers();
    }
  };
  </script>
  
  <style scoped>
  body, html {
      font-family: cursive;
      background-color: #F7F7F7; 
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
  }
  
  header {
      background-color: #3E3E3E; 
      padding: 10px;
      width: 100%;
      display: flex;
      justify-content: center;
      border-radius: 15px;
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1); 
  }
  
  .post-component {
      margin-top: 50px; 
  }
  
  .post-container {
      margin-top: 20px;
      max-height: 500px; 
      overflow-y: auto; 
  }
  
  .post {
      margin-bottom: 20px;
      padding: 20px; 
      background-color: #FFFFFF;
      border-radius: 8px;
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .no-posts {
      color: #999;
      font-style: italic; 
      margin-top: 10px; 
  }
  </style>
  
  