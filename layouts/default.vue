<template>
  <div>
    <Nuxt />
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
html {
  font-family: 'Montserrat', sans-serif;
  /* font-size: 1.25rem; */
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  background: #181818;
  /* solves mobile scaling issue, but still don't know the cause... */
  overflow-x: hidden;
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
                        supported by Chrome, Edge, Opera and Firefox */
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

::-webkit-scrollbar {
  display: none;
}

.button--green {
  display: inline-block;
  margin: 0.25em;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  margin: 0.25em;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}

.container {
  height: auto;
  width: 100%;
  display: flex;
  align-items: center;
  text-align: center;
}

.logo {
}

.nav a {
}

.links {
}

.posts {
  max-width: 35rem;
  /* prevents the width from being 100% on mobile / smaller screens */
  width: 95%;
}

.container h2 {
}

.container ul {
}

.container p {
}

.container a {
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
