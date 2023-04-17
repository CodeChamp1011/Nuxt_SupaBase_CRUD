<template>
  <div
    id="toast-simple"
    class="fixed items-center w-full max-w-xs p-4 space-x-4 text-gray-500 bg-white divide-x divide-gray-200 rounded-lg shadow dark:text-gray-400 dark:divide-gray-700 space-x dark:bg-gray-800 top-10 right-10"
    role="alert"
    v-if="show"
  >
    <div class="pl-4 text-medium whitespace-nowrap dark:text-white font-normal">
      {{ message }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: false,
      message: "",
      color: "",
    };
  },

  methods: {
    showNotification(message, color) {
      this.message = message;
      this.color = color;
      this.show = true;

      setTimeout(() => {
        this.hideNotification();
      }, 5000);
    },

    hideNotification() {
      this.show = false;
      this.message = "";
      this.color = "";
    },
  },
};
</script>
