<template>
  <div class="header" id="header">
    <div class="logo">
      <img src="../assets/logo.png" />
    </div>
    <div class="hello">
      <h2>Hello<br />I am<br />Eslam</h2>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.header {
  background-color: #222;
  color: #eee;

  .logo {
    width: 100px;
    display: inline-block;
    margin: 20px;

    img {
      width: 100%;
    }
  }

  .hello {
    h2 {
      font-size: 80px;
      margin: 150px 0 0 50%;
    }
  }
}

@media (max-width: 600px) {
  h2 {
    margin: 150px 20px 0 !important;
  }
}
</style>
