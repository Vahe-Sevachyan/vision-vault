<template>
  <main>
    <div class="overlay"></div>
    <div class="container">
      <header>
        <h1>Vision Vault</h1>
        <button>+</button>
      </header>
      <div class="cards-container">
        <div class="card">
          <p class="main-text">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure porro
            fuga explicabo, officia incidunt qui?
          </p>
          <p class="date">02/22/2022</p>
        </div>
        <div class="card">
          <p class="main-text">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure porro
            fuga explicabo, officia incidunt qui?
          </p>
          <p class="date">02/22/2022</p>
        </div>
      </div>
    </div>
  </main>
</template>
<script setup></script>
<style scoped>
main {
  height: 100vh;
  width: 100vw;
}
.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 35px;
}
button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: black;
  color: white;
  border-radius: 50%;
  font-size: 25px;
}
.card {
  width: 225px;
  height: 225px;
  background-color: orange;
  padding: 10px;
  border-radius: 15px;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.main-text {
  margin-bottom: 110px;
}

.cards-container {
  display: flex;
  flex: wrap;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
