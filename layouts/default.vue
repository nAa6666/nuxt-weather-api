<template>
  <div class="default">
    <Header/>
    <div class="container">
      <slot />
    </div>
    <Footer/>
  </div>
</template>

<style>
  body{
    margin: 0;
  }
  .container{
    max-width: 1145px;
    width: 100%;
    padding: 60px 15px 0;
    margin: auto;
  }
</style>