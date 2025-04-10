<template>
  <div>
    <div class="header">
      <slot name="header"></slot>
    </div>
  </div>

  <div v-for="(admin, index) in allAdmins" :key="index" class="admin-section">
    <div class="admin">
      <div class="data">
        <h3>id : {{ admin.id + 1 }}</h3>
        <h3>Name : {{ admin.name }}</h3>
        <h3>Age : {{ admin.age }}</h3>
      </div>
      <div class="delte-btn">
        <button @click="$emit('DleteAdmin', admin.id)">delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AdminComp",
  props: ["allAdmins"],
  //   inject: ["allAdmins"],
};
</script>

<style scoped>
.admin-section {
  display: flex;
  flex-direction: column;
  font-size: 1.8rem;
}

.admin {
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
