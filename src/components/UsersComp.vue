<template>
  <div>
    <div class="header">
      <slot name="header"></slot>
    </div>
  </div>

  <div v-for="(user, index) in allUsers" :key="index" class="user-section">
    <div class="user">
      <div class="data">
        <h3>id : {{ user.id + 1 }}</h3>
        <h3>Name : {{ user.name }}</h3>
        <h3>Age : {{ user.age }}</h3>
      </div>
      <div class="delte-btn">
        <button @click="$emit('DleteUser', user.id)">delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UsersComp",
  props: ["allUsers"],
  //   inject: ["allUsers"],
  methods: {
    displayallUsers() {
      console.log("Users");
      console.log(this.allUsers);
    },
  },
};
</script>

<style scoped>
.user-section {
  display: flex;
  flex-direction: column;
  font-size: 1.8rem;
}

.user {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: rgb(8, 37, 37);
  margin: 1rem 0;
  color: white;
  padding: 1.6rem 3.6rem;
}

.delte-btn button {
  padding: 1rem 1.4rem;
  font-size: 1.6rem;
  background-color: red;
  color: white;
  border: none;
  cursor: pointer;
}

.data h3 {
  padding: 0.8rem;
}
</style>
