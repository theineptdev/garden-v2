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

::-webkit-scrollbar {
  display: none;
}

.container {
  height: auto;
  width: 100%;
  display: flex;
  align-items: center;
  text-align: center;
}

.posts {
  max-width: 35rem;
  /* prevents the width from being 100% on mobile / smaller screens */
  width: 95%;
}

.container a {
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
