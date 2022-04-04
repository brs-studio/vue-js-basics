<template>
  <div class="board">
   <div class="about">
    <router-link to="/">Home</router-link>
    <br>
    <router-link to="/about">About</router-link>
    </div>
    <br>
    <h1> About the app </h1>
    <p>
      This is the trello board: We can add the task related details.It has
      columns to rearrange the tasks between Inprogress, todo, done.
    </p>
  </div>
</template>
<style scoped>
.about {
  margin-top: 30px;
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}
</style>
