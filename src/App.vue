<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <main>
    <router-view></router-view>
  </main>
</template>


<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
*{
  margin: 0;
  padding:0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
  font-weight: 400;
  font-style: normal;
}

body{
  background-color: #35495E;
}

a{
  text-decoration: none;
}

header{
  display: flex;
  align-items: center;
  justify-content:center;
  padding: 10px 16px;
  background-color: #2C3D4E;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
}

header h1{
  color: #FFF;
  font-size: 28px;
}

header h1 span{
  color: #42b883;
}

</style>