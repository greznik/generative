<template>
  <div id="app">
    <header class="header">
      <h1>
        <router-link to="/">George<span>Reznik</span></router-link>
      </h1>
    </header>
    <router-view />
  </div>
</template>

<style>
html {
  background: #222;
}
body {
  margin: 0;
  overflow: hidden;
  color: #eee;
  font-family: "Raleway", sans-serif;
  font-weight: 200;
}
.header {
  padding-left: 5px;
  padding-right: 5px;
  border-bottom: 1px solid #eee;
  align-items: center;

  text-transform: uppercase;
}
a {
  text-decoration: none;
  color: #eee;
}
h1 {
  font-size: 14px;
}
h1 span,
h2 span {
  color: #fc3;
  font-weight: 600;
}
</style>
