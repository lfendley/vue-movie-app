<template>
  <header>
    <div class="container">
      <router-link to="/">
        <h1>TAPE</h1>
      </router-link>
    </div>
  </header>
  <main>
    <router-view />
  </main>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Monoton&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Raleway', sans-serif;

  &::selection {
    background: transparentize($color: #d66060, $amount: 0.5)
  }
}

body {
  background-color: #282931;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  padding: 5px;
  background-color: #282931;
  box-shadow: 0px 0px 6px rgba(0,0,0,0.1);

  h1 {
    color: #d64f55;
    font-size: 44px;
    font-family: 'Monoton', cursive;
  }
}

.container {
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
@media (min-width: 768px) {
  .container {
    width: 750px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1170px;
  }
}

</style>