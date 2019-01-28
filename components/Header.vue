<template>
    <div class="header menu nav navbar navbar-expand-lg navbar-dark">
      <nuxt-link to="/" class="navbar-brand"><b>暗号メーカー 〜ango!〜</b></nuxt-link>
      <nuxt-link to="/info" class="nav-link">
        <b>このサイトについて</b>
      </nuxt-link>
    </div>
</template>

<style>
  .header {
    font-size: 20px;
    left: 0;
    top: 0;
    width: 100%;
    height: 50px;
    background-color: #5bffff;
    color: white;
    text-align: left;
    padding: 15px;
  }

  .header a {
    text-decoration: none;
  }

  .header a:link,
  .header a:visited {
    color: #fff;
  }
</style>