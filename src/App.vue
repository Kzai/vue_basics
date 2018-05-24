<template>
  <div id="app">
  <div class="noteContainer">
    <div class="orangeNote note"></div>
    <div class="note">Orange = App component</div>
  </div>

  <div class="noteContainer">
    <div class="greenNote note"></div>
    <div class="note">Green = Parent component</div>
  </div>

  <div class="noteContainer">
    <div class="pinkNote note"></div>
    <div class="note">Pink = Child component</div>
  </div>

  <div class="noteContainer">
    <div class="yellowNote note"></div>
    <div class="note">Yellow = Grandchild component</div>
  </div>
    <p>(Make this pane full height for best viewing experience)</p>

    <Parent/>
  </div>
</template>

<script>
import Parent from "./components/Parent";

export default {
  name: "App",
  components: {
    Parent
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
  padding: 2rem;
  height: 100%;
  border: orange 5px solid;
}
.noteContainer {
  font-size: 0.865rem;
  display: inline-flex;
}
.orangeNote {
  height: 1rem;
  width: 1rem;
  background-color: orange;
  margin-right: 0.5rem;
}
.pinkNote {
  height: 1rem;
  width: 1rem;
  background-color: #db2dff;
  margin-right: 0.5rem;
}
.greenNote {
  height: 1rem;
  width: 1rem;
  background-color: #80ff00;
  margin-right: 1rem;
}

.yellowNote {
  height: 1rem;
  width: 1rem;
  background-color: #ffde00;
  margin-right: 1rem;
}

p {
  font-size: 0.865rem;
}

.note {
  margin-right: 0.5rem;
}
</style>
