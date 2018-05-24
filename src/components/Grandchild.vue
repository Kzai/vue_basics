<template>
  <div class="helloGrandchild">
    <div class="messageContainer">
        <h1>Grandma says:</h1>
        <h1 class="fromGrandma">'{{grandmaSays}}'</h1>
    </div>
    <div class="messageContainer">
        <h1>My mother says:</h1>
        <h1 class="fromMom">'{{momSays}}'</h1>
    </div>
    <button 
      :class="{'thief': amIaThief, 'angel': !amIaThief }" 
      @click="emitEventToParent">
      {{buttonText}}
    </button>
  </div>
</template>

<script>
export default {
  name: "Grandchild",
  props: ["grandmaSays", "momSays"],
  data() {
    return {
      messageForMyGrandma: "",
      messageForMyMom: "",
      amIaThief: false
    };
  },
  methods: {
    emitEventToParent: function() {
      if (this.amIaThief) {
        this.messageForMyGrandma = "Can I have some money, grandma!";
        this.messageForMyMom = "Let's rob grandma's purse.";
        // handle data and give it back to parent by interface
      } else {
        this.messageForMyGrandma = "You are a stinking lier!";
        this.messageForMyMom = "What should we spend the money on?";
      }
      this.amIaThief = !this.amIaThief;
      //Like a publish / subscribe channel
      this.$emit(
        "interface",
        this.messageForMyGrandma,
        this.messageForMyMom,
        this.amIaThief
      );
    }
  },
  computed: {
    buttonText: function() {
      let text = "";
      if (this.amIaThief) {
        text = "Put back";
      } else {
        text = "Steal purse";
      }
      return text;
    }
  },
  // lifecycle methods
  init() {},
  beforeCreate() {},
  created() {},
  beforeMount() {},
  mounted() {},
  beforeDestroy() {},
  destroyed() {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  border: #ffde00 3px solid !important;
}
.helloGrandchild {
  border: #ffde00 6px solid !important;
  color: black;
  background-color: #fff799;
  height: 100%;
}
h1 {
  color: black;
  font-size: 1rem;
}
.messageContainer {
  width: 100%;
  display: inline-flex;
}

.fromGrandma {
  color: #80ff00;
  background-color: black;
}
.fromMom {
  background-color: black;
  color: #ed9ffd;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}
.grandchildInput {
  height: 2rem;
  margin-top: 0.25rem;
  font-size: 1rem;
  margin-left: 1rem;
}
.thief {
  font-size: 1rem;
  width: 8rem;
  height: 3rem;
  color: white;
  background-color: blue;
}
.angel {
  font-size: 1rem;
  width: 8rem;
  color: white;
  height: 3rem;
  background-color: red;
}
</style>
