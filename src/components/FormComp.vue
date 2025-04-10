<template>
  <div class="container">
    <div class="theme-section">
      <button class="theme-btn" @click="$emit('Theme')">Generate Theme</button>
    </div>
    <div class="buttons">
      <button @click="displayForm()">Form</button>
      <button @click="displayUsers()">users</button>
      <button @click="displayAdmins()">admins</button>
    </div>

    <div v-if="formFlag" class="form">
      <h1 class="header">Form</h1>
      <div class="form-sec">
        <div class="input-field">
          <label for="inputName">Input Name</label>
          <input type="text" id="inputName" v-model.trim="inputData.name" />
        </div>

        <div class="input-field">
          <label for="age"
            >Input Age<span style="visibility: hidden">fff</span></label
          >
          <input type="number" id="age" v-model.number="inputData.age" />
        </div>

        <div class="input-field role">
          <div class="choice">
            <input
              type="radio"
              name="role"
              value="Admin"
              id="admin"
              v-model="inputData.type"
            />
            <label for="admin">Admin</label>
          </div>

          <div class="choice">
            <input
              type="radio"
              name="role"
              value="User"
              id="user"
              v-model="inputData.type"
            />
            <label for="user">user</label>
          </div>
        </div>
        <div class="submit-btn" @click="hanldeInputData()">
          <button>Submit</button>
        </div>
      </div>
    </div>

    <UserComp v-if="userFlag" @DleteUser="deleteUser" :allUsers="usersArray">
      <template v-slot:header>
        <h1 class="header">{{ userHeader }}</h1>
      </template>
    </UserComp>

    <AdminComp
      v-if="adminFlag"
      @DleteAdmin="deleteAdmin"
      :allAdmins="adminArray"
    >
      <template v-slot:header>
        <h1 class="header">{{ adminHeader }}</h1>
      </template>
    </AdminComp>
  </div>
</template>

<script setup></script>

<script>
import UserComp from "./UsersComp.vue";
import AdminComp from "./AdminsComp.vue";

export default {
  name: "FormComp",
  components: { UserComp, AdminComp },
  data() {
    return {
      userHeader: "Users",
      adminHeader: "Admins",
      formFlag: true,
      userFlag: false,
      adminFlag: false,
      usersArray: [],
      adminArray: [],
      usersIndex: 0,
      adminIndex: 0,
      inputData: {
        name: "",
        age: "",
        type: "",
      },
    };
  },
  methods: {
    displayForm() {
      this.formFlag = true;
      this.userFlag = false;
      this.adminFlag = false;
    },
    displayUsers() {
      this.formFlag = false;
      this.userFlag = true;
      this.adminFlag = false;
    },
    displayAdmins() {
      this.formFlag = false;
      this.userFlag = false;
      this.adminFlag = true;
    },
    addAdmin() {
      const newAdmin = { ...this.inputData, id: this.adminIndex };
      this.adminArray.push(newAdmin);
      this.adminIndex++;
      console.log(this.adminArray);
    },
    addUser() {
      const newUser = { ...this.inputData, id: this.usersIndex };
      this.usersArray.push(newUser);
      this.usersIndex++;
      console.log(this.usersArray);
    },
    hanldeInputData() {
      this.inputData.name =
        this.inputData.name === "" ? "Dummy" : this.inputData.name;
      this.inputData.age = this.inputData.age === "" ? 22 : this.inputData.age;

      if (this.inputData.type === "User") {
        this.addUser();
      } else if (this.inputData.type === "Admin") {
        this.addAdmin();
      } else {
        this.inputData.type = "User";

        this.addUser();
      }
      this.inputData = {
        name: "",
        age: "",
        type: "",
      };
    },
    deleteUser(index) {
      this.usersArray = this.usersArray.filter((user) => user.id !== index);
      console.log("delete user", this.usersArray);
    },

    deleteAdmin(index) {
      this.adminArray = this.adminArray.filter((admin) => admin.id !== index);
      console.log("delete admin", this.adminArray);
    },
  },
  provide() {
    return {
      allUsers: this.usersArray,
      allAdmins: this.adminArray,
    };
  },
};
</script>

<style scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.header {
  color: white;
  background-color: blue;
  padding: 1.8rem;
}

.theme-section {
  display: flex;
  margin: 0;
  padding: 0;
}
.buttons {
  display: flex;
  justify-content: space-evenly;
  margin-bottom: 1.6rem;
}

.buttons button,
.theme-btn {
  padding: 1.2rem 1.7rem;
  cursor: pointer;
  font-size: 1.8rem;
  border: none;
  background-color: #09c;
  color: white;
}

.theme-btn {
  padding: 0.8rem 1.2rem;
  background-color: blueviolet;
}

.form-sec {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 40vh;
  padding: 1.8rem 1.3rem;
  /* background-color: red; */
  font-size: 1.8rem;
}

.input-field label {
  margin-right: 1.8rem;
}

.input-field {
  display: flex;
  justify-content: flex-start;
  width: 80%;
  margin: auto;
  padding: 0.9rem;
}

.input-field input {
  width: 80%;
  font-size: 1.6rem;
  padding: 0.7rem 1.2rem;
  border-radius: 1.4rem;
  transition: all 0.2s;
}

.input-field input:focus {
  outline-color: blue;
}

.input-field label {
  font-size: 1.6rem;
  padding: 0.7rem 1.2rem;
  font-weight: 700;
}
.input-field .choice {
  display: flex;
  gap: 15px;
  font-size: 1.8rem;
  justify-content: center;
  align-items: center;
}

input[type="radio"] {
  width: 1.8rem;
  height: 1.8rem;
}

.submit-btn {
  width: 80%;
}

.submit-btn button {
  margin: 1.7rem auto;
  padding: 1rem 1.7rem;
  cursor: pointer;
  width: 50%;
  font-size: 1.6rem;
  background-color: rgb(17, 52, 53);
  color: white;
  transition: all 0.3s;
}

.submit-btn button:hover {
  background-color: green;
}
</style>
