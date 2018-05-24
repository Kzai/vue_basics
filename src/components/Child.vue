<template>
  <div class="helloChild">
    <!--Insert snippet stuff here-->
    <div class="messageContainer">
      <h1>My mother says:</h1>
      <h1 class="inheritedProp">{{messageFromParent}}</h1>
    </div>
    <div class="messageContainer">
      <h1 class="">My child says:</h1>
      <h1 class="childEmitValue">{{messageFromChild}}</h1>
    </div>
    <!-- The grandchild component is a direct child of this control. 
    It is a 'nested control' of the grandparent -->
    <div class="grandchildComponentContainer">
      <grandchild
        v-bind:grandmaSays="messageForGrandchild"
        v-bind:momSays="messageForChild"
        @interface="handleEventFromChild">
      </grandchild>
    </div>
  </div>
</template>

<script>
import Grandchild from "../components/Grandchild.vue";
export default {
  name: "Child",
  // props are inherited from parent, bound to the child component when defined in parent template HelloWorld.vue
  props: ["messageFromParent", "messageForGrandchild"],
  components: { Grandchild },
  data() {
    // data properties must be declared, then may be assigned at runtime - null
    return {
      msg: "Hey",
      comp: null,
      messageFromChild: "Lets rob grandma's purse!",
      messageForMom: "Can I have some money, mom?",
      messageForChild: "Yes! Quick, she's not looking! Take it and run!",
      isMomsPurseMissing: false
    };
  },
  methods: {
    handleEventFromChild: function(
      messageForMyMomFromMyChild,
      messageForMe,
      isMyChildaThief
    ) {
      this.messageFromChild = messageForMe;
      this.isMomsPurseMissing = isMyChildaThief;
      if (!isMyChildaThief) {
        this.messageForMom = "Can I have some money mom?";
        this.messageForChild = "Yes! Quick, she's not looking! Run!";
      } else {
        this.messageForMom = "How dare you accuse my little angel!";
        this.messageForChild = "You did good, kid! Let's get ice-cream";
      }
      //isMomsPurseMissing should be set by parent - not equal to isMyChildaThief?

      //Emit a message for grandma that is dependent on what grandchild says
      this.$emit(
        "interface",
        messageForMyMomFromMyChild,
        this.messageForMom,
        isMyChildaThief
      );
    }
  },
  // Computed values prepare data for the view template or can assign values to data properties
  computed: {
    didMyChildSteal: function() {
      return !this.isMomsPurseMissing;
    }
  },
  // Each component has lifecycle methods
  init() {},
  beforeCreate() {},
  created() {},
  // Before the component is mounted, we can calculate some propeties
  beforeMount() {
    this.isMomsPurseMissing = this.didMyChildSteal;
  },
  mounted() {},
  beforeDestroy() {},
  destroyed() {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  border: #db2dff 3px solid;
}
.helloChild {
  color: white;
  background-color: #f4bdff;
  height: 100%;
  padding: 1rem;
  /* margin-top: 1rem; */
}
.comp {
  color: black;
  height: 3rem;
}

.toggleClassesDiv {
  width: 90%;
  height: 3rem;
  margin: 1rem 5% 1rem 5%;
  text-align: center;
}
.target {
  color: black;
  font-size: 2rem;
  height: 3rem;
}
.red {
  background-color: red;
  color: black;
}
.blue {
  background-color: blue;
}

.bigButton {
  width: 12rem;
  height: 3rem;
  background-color: black;
  color: white;
  margin-top: 1rem;
  margin-bottom: -1rem;
}

.messageContainer {
  width: 100%;
  display: inline-flex;
}

.inputBox {
  height: 2rem;
  width: 50%;
}

.inheritedProp {
  background-color: black;
  font-size: 1rem;
  color: #80ff00;
  margin-left: 0.5rem;
}
.childEmitValue {
  color: #ffde00;
  background-color: black;
  font-size: 1rem;
  margin-left: 0.5rem;
}
.grandchildComponentContainer {
  /* margin-left: 2%; */
  width: 96%;
  margin: 2%;
}

p {
  color: black;
  font-size: 0.865rem;
}

h1 {
  font-weight: normal;
  color: black;
  font-size: 1rem;
  font-weight: 700;
}
h2 {
  font-weight: normal;
  color: black;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
