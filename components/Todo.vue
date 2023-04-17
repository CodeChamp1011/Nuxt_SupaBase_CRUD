<!-- Please remove this file from your project -->
<template>
  <div scope="row" class="flex items-center bg-black justify-center h-screen">
    <Notification ref="notification" />
    <div class="relative overflow-x-auto shadow-md sm:rounded-lg">
      <h1 class="flex justify-center text-green-500 text-4xl font-bold">
        Nuxt.js + Supabase
      </h1>
      <br />
      <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead
          class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
        >
          <tr>
            <th scope="col" class="px-6 py-3 dark:text-white">Name</th>
            <th scope="col" class="px-6 py-3 dark:text-white">UserName</th>
            <th scope="col" class="px-6 py-3 dark:text-white">Email</th>
            <th scope="col" class="px-6 py-3 dark:text-white">Dummy</th>
            <th scope="col" class="px-6 py-3 dark:text-white">Login Date</th>
            <th scope="col" class="px-6 py-3 dark:text-white">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="item in items"
            :key="item.id"
            class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
              {{ item.name }}
            </th>
            <td
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
              {{ item.username }}
            </td>
            <td
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
              {{ item.email }}
            </td>
            <td
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
              {{ item.dummy }}
            </td>
            <td
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
            >
              {{ item.login_date }}
            </td>
            <td class="px-6 py-4">
              <button
                type="button"
                class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 font-medium rounded-lg text-sm px-4 py-0.5 text-center mr-2 mb-2"
                @click="removeUser(item.id)"
              >
                Remove
              </button>
              <button
                type="button"
                class="text-gray-900 bg-gradient-to-r from-teal-200 to-lime-200 hover:bg-gradient-to-l hover:from-teal-200 hover:to-lime-200 focus:ring-4 focus:outline-none focus:ring-lime-200 dark:focus:ring-teal-700 font-medium rounded-lg text-sm px-4 py-0.5 text-center mr-2 mb-2"
                value="Edit"
                @click="Editmodal(item.id)"
              >
                Edit
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="flex justify-center mt-2">
        <button
          type="button"
          @click="Addmodal()"
          data-modal-target="user-modal"
          data-modal-toggle="user-modal"
          class="text-white bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
        >
          Add User
        </button>
        <div
          v-if="showModal"
          class="fixed inset-0 flex items-center justify-center overflow-auto bg-black bg-opacity-50 z-50 transition-opacity ease-out duration-300"
        >
          <div class="bg-white rounded p-6 mx-auto w-full md:w-1/2">
            <h3 id="title" class="text-2xl font-bold">{{ this.user }}</h3>
            <div class="px-6 py-2 lg:px-8">
              <form class="space-y-2">
                <div>
                  <label
                    for="name"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Your name</label
                  >
                  <input
                    type="input"
                    name="name"
                    id="name"
                    v-model="form.name"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 text-gray-900 dark:text-black"
                    placeholder="Michael Elliott"
                    required
                  />
                </div>
                <div>
                  <label
                    for="username"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Your username</label
                  >
                  <input
                    type="input"
                    name="username"
                    id="username"
                    v-model="form.userName"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 text-gray-900 dark:text-black"
                    placeholder="Michael Elliott"
                    required
                  />
                </div>
                <div>
                  <label
                    for="email"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Your email</label
                  >
                  <input
                    type="email"
                    name="email"
                    id="email"
                    v-model="form.email"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 text-gray-900 dark:text-black"
                    placeholder="name@company.com"
                    required
                  />
                </div>
                <div>
                  <label
                    for="dummy"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Your dummy</label
                  >
                  <input
                    type="input"
                    name="dummy"
                    id="dummy"
                    v-model="form.dummy"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 text-gray-900 dark:text-black"
                    placeholder="Dummy"
                    required
                  />
                </div>
              </form>
            </div>
            <div class="flex justify-center mt-2">
              <button
                id="adduser"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 mr-2 rounded"
                @click="addUser()"
              >
                {{ this.button }}
              </button>
              <button
                @click="showModal = false"
                class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded"
              >
                Close
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { createClient } from "@supabase/supabase-js";
import Notification from "./Notification.vue";

const supabaseUrl = "https://bxdwaytmnahfvctkoipf.supabase.co";
const supabaseKey =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ4ZHdheXRtbmFoZnZjdGtvaXBmIiwicm9sZSI6ImFub24iLCJpYXQiOjE2ODE0NzAxNDAsImV4cCI6MTk5NzA0NjE0MH0.gkIyxs0jyGJaVZkSj4oEATcK--8X3KZCrFfVphCpUyg";

export default {
  components: {
    Notification,
  },
  data() {
    return {
      items: [],
      Id: 0,
      user: "Add User",
      button: "Add User",
      showModal: false,
      form: {
        name: "",
        userName: "",
        email: "",
        dummy: "",
      },
    };
  },

  async created() {
    this.supabase = createClient(supabaseUrl, supabaseKey, { mode: "cors" });

    const { data, error } = await this.supabase.from("users").select("*");

    if (error) {
      console.error(error);
    } else {
      this.items = data;
    }
  },
  methods: {
    async getAllUser() {
      const { data, error } = await this.supabase.from("users").select("*");
      if (error) {
        console.error(error);
      } else {
        this.items = data;
      }
    },
    async removeUser(rowId) {
      const tableName = "users";
      const { data, error } = await this.supabase
        .from(tableName)
        .delete()
        .eq("id", rowId)
        .select("*");

      if (error) {
        console.log("Error deleting data: ", error);
      } else {
        this.$refs.notification.showNotification(
          "Successfully Deleted",
          "green"
        );
        this.showModal = false;
        this.getAllUser();
        this.$refs.notification.showNotification(
          "Successfully Deleted",
          "green"
        );
      }
    },
    async addUser() {
      const tableName = "users";
      const name = this.form.name;
      const username = this.form.userName;
      const email = this.form.email;
      const dummy = this.form.dummy;
      const login_date = new Date().toLocaleDateString();
      if (document.getElementById("title").textContent === "Edit User") {
        console.log(this.Id, name, username, email, dummy, login_date);

        const data = {
          name: name,
          username: username,
          email: email,
          dummy: dummy,
        };
        console.log(data);
        const { data: updatedRows, error } = await this.supabase
          .from(tableName)
          .update(data)
          .eq("id", this.Id);

        if (error) {
          console.log(error);
        } else {
          this.showModal = false;
          this.getAllUser();
          this.$refs.notification.showNotification(
            "Successfully Updated",
            "green"
          );
        }
      } else {
        const { error } = await this.supabase
          .from(tableName)
          .insert({ name, username, email, dummy, login_date });
        if (error) {
          console.log(error);
        } else {
          this.showModal = false;
          this.getAllUser();
          this.$refs.notification.showNotification(
            "Successfully Created",
            "green"
          );
        }
      }
    },

    Addmodal() {
      this.showModal = "true";
      this.user = "Add User";
      this.button = "Add User";
      this.form.name = "";
      this.form.userName = "";
      this.form.email = "";
      this.form.dummy = "";
    },

    async Editmodal(rowId) {
      this.showModal = true;
      this.user = "Edit User";
      this.button = "Edit User";
      this.Id = rowId;
      const tableName = "users";
      const { data, error } = await this.supabase
        .from(tableName)
        .select("*")
        .eq("id", rowId);
      this.form.name = data[0].name;
      this.form.userName = data[0].username;
      this.form.email = data[0].email;
      this.form.dummy = data[0].dummy;
    },
  },
};
</script>
