<script setup>
  import { RouterView } from 'vue-router'
 
</script>

<template>
  <header>
    <router-link to="/">
        <h1><span>Movies</span>App</h1>

    </router-link>
  </header>
  <main>
    <RouterView />
  </main>
 
</template>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;

    &::selection{
      background: transparentize(#8b0a0a, 0.5);
    }
  }

  body{
    background-color: #ffffff;
  }

  a{
    text-decoration: none;
  }

  header{
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px 16px;
    background-color: #345678;
    box-shadow: 0px 0px 6px rgba(0,0,0,0.2);
  }

  h1{
    color: #ffff;
    font-size: 24px;

    span{
      color: #8b0a0a;
    }
  }
</style>
