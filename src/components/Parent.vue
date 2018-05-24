<template>
  <div class="helloParent">
    <!--Vue uses double moustaches to outut data properties-->
    <h1 class="componentTitle">{{ whoIam }}</h1>
    <div class="grandmasPurseContainer">
      <!-- Note: use of v-if and v-else directives -->
      <div v-if="!purseMissing" class="purseContainer">
        <img class="grandmasPurse" src="https://www.svgrepo.com/show/99351/purse.svg" alt="">
        <h3 class="whosPurse">{{grandmaShouts}}</h3>
      </div>
      <div v-else class="purseContainer">
        <img class="grandmasPurse" src="http://www.i2clipart.com/cliparts/c/7/3/d/clipart-scream-face-icon-512x512-c73d.png" alt="">
        <h3 class="whosPurse">{{grandmaShouts}}</h3>
      </div>
    </div>
    <div class="grandchildMessageContainer">
        <h3>My grandchild says:</h3>
        <h3 class="messageFromGrandchildText">{{messageFromGrandchild}}</h3>
    </div>
     <div class="childMessageContainer">
        <h3>My child says:</h3>
        <h3 class="messageFromChildText">{{messageFromChild}}</h3>
    </div>
    <div class="childComponentContainer">
      <!--we can bind data here in parent to child component and give it a reference name -->
      <child-element 
        v-bind:messageFromParent="grandmaToChild" 
        v-bind:messageForGrandchild="grandmaToGrandchild"
        @interface="handleEventFromChild">
      </child-element>
    </div>
    
  </div>
</template>

<script>
//import child componenents here
import Child from "../components/Child.vue";
export default {
  name: "Parent",
  //list the child components here
  components: { "child-element": Child },
  //data is always a function
  data() {
    return {
      whoIam: "I am the parent component. I am Grandma",

      shout: "",
      sayToChild: "",
      sayToGrandChild: "",

      purseMissing: false, //Grandma has her purse
      messageFromGrandchild: "Can I have some money, grandma?",
      messageFromChild: "Can I have some money, mom?"
    };
  },
  methods: {
    myPurseWasSnatched: function() {
      this.purseMissing = true;
    },
    myPurseWasReturned: function() {
      this.purseMissing = false;
    },
    togglePurseMissing: function() {
      this.purseMissing = !this.purseMissing;
    },
    handleEventFromChild: function(
      messageFromGrandchild,
      messageFromMyChild,
      isGrandchildThief
    ) {
      this.messageFromGrandchild = messageFromGrandchild;
      this.messageFromChild = messageFromMyChild;
      if (isGrandchildThief) {
        this.myPurseWasSnatched();
      } else {
        this.myPurseWasReturned();
      }
    }
  },
  computed: {
    grandmaShouts: function() {
      let message = "";
      if (!this.purseMissing) {
        message = "I'm rich!";
      } else {
        message = "O.M.G! My purse is gone!";
      }
      return message;
    },
    grandmaToChild: function() {
      let message = "";
      if (!this.purseMissing) {
        message = "No. No money for you.";
      } else {
        message = "Your child is a thief - he stole my purse!";
      }
      return message;
    },
    grandmaToGrandchild: function() {
      let message = "";
      if (!this.purseMissing) {
        message = "No. You cannot have any money.";
      } else {
        message = "You little punk! Give me back my purse!";
      }
      return message;
    }
  },
  beforeMount() {
    this.shout = this.grandmaShouts;
    this.sayToChild = this.grandmaToChild;
    this.sayToGrandchild = this.grandmaToGrandchild;
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  background-color: green;
  border: #80ff00 1px solid;
}
.helloParent {
  margin-top: 1rem;
}
h1,
h2 {
  font-weight: normal;
  color: white;
}
.componentTitle {
  font-size: 1.5rem;
  margin-bottom: -1rem;
}
h3 {
  margin-top: -1.25rem;
  color: white;
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
.grandmasPurseContainer {
  display: inline;
}
.grandchildMessageContainer {
  display: inline-flex;
}
.childMessageContainer {
  display: inline-flex;
}
.purseContainer {
  width: 20%;
  margin-left: 40%;
  min-height: 200px;
  max-height: 200px;
}
.grandmasPurse {
  background-color: white;
  height: 120px;
}
.emptyDiv {
  height: 120px;
}
.whosPurse {
  margin-top: 0.5rem;
  font-size: 1.25rem;
  min-height: 3rem;
  max-height: 3rem;
}
.messageFromGrandchildText {
  background-color: black;
  color: yellow;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}
.messageFromChildText {
  background-color: black;
  color: #db2dff;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}
.childComponentContainer {
  padding: 1rem;
}
</style>
