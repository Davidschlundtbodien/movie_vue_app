<template>
  <div class="home">
    <h1>Actors</h1>
    <h1>New Actor</h1>
    <div>
      First Name: <input type="text" v-model="newActorFirstName"><br>
      Last Name: <input type="text" v-model="newActorLastName"><br>
      Age: <input type="number" v-model="newActorAge"><br>
      Gender: <input type="text" v-model="newActorGender"><br>
      Known For: <input type="text" v-model="newActorKnownFor"><br>
      <button v-on:click="createActor()">Create Actor</button>
    </div>
    <div v-for="actor in actors">
      <h2>{{ actor.first_name }} {{actor.last_name}}</h2>
      <button v-on:click="showActor(actor)">Show more</button>
      <div v-if="currentActor === actor">
        <p>Age: {{ actor.age }}</p>
        <p>Gender: {{ actor.gender }}</p>
        <p>Known For: {{ actor.known_for }}</p>
        <div>
          <h3>Update actor</h3>
          First Name: <input type="text" v-model="actor.first_name"><br>
          Last Name: <input type="text" v-model="actor.last_name"><br>
          Age: <input type="number" v-model="actor.age"><br>
          Gender: <input type="text" v-model="actor.gender"><br>
          Known For: <input type="text" v-model="actor.known_for"><br>
          <button v-on:click="updateActor(actor)">Update Actor</button><button v-on:click="destroyActor(actor)">Remove Actor</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      currentActor: {},
      actors: [],
      newActorFirstName: "",
      newActorLastName: "",
      newActorAge: "",
      newActorGender: "",
      newActorKnownFor: ""
    };
  },
  created: function() {
    axios.get("/api/actors").then(response => {
      this.actors = response.data;
    });
  },
  methods: {
    createActor: function() {
      var params = {
        first_name: this.newActorFirstName,
        last_name: this.newActorLastName,
        age: this.newActorAge,
        gender: this.newActorGender,
        known_for: this.newActorKnownFor,
        movie_id: 1
      };
      axios.post("/api/actors", params).then(response => {
        this.actors.unshift(response.data);
        this.newActorFirstName = "";
        this.newActorLastName = "";
        this.newActorAge = "";
        this.newActorGender = "";
        this.newActorKnownFor = "";
      });
    },
    showActor: function(actor) {
      if (this.currentPhoto === actor) {
        this.currentActor = {};
      } else {
        this.currentActor = actor;
      }
    },
    updateActor: function(actor) {
      var params = {
        id: actor.id,
        first_name: actor.first_name,
        last_name: actor.last_name,
        age: actor.age,
        gender: actor.gender,
        know_for: actor.know_for
      };
      axios.patch("/api/actors/" + actor.id, params).then(response => {
        this.currentActor = {};
      });
    },
    destroyActor: function(actor) {
      axios.delete("/api/actors/" + actor.id).then(response => {
        var index = this.actors.indexOf(actor.id);
        this.actors.splice(index, 1);
      });
    }
  }
};
</script>