<template>
  <li>
    <h2>{{ friend.name }} {{ friend.isFavorite ? "(Favorite)" : "" }}</h2>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <button @click="toggleFavorite">Toggle Favorite</button>
    <ul v-if="detailsAreVisible">
      <li><strong>Phone:</strong> {{ friend.phone }}</li>
      <li><strong>Email:</strong> {{ friend.email }}</li>
    </ul>
  </li>
</template>

<script>
export default {
  //   props: ["friend"],
  props: {
    friend: {
      id: { type: String, required: true },
      name: { type: String, required: true },
      phone: { type: String, required: true },
      email: { type: String, required: true },
      isFavorite: {
        // type: String,
        // required: false,
        // default: "0",
        // validator: (value) => value === "1" || value === "0",
        type: Boolean,
        required: false,
        default: false,
      },
    },
  },
  data() {
    return {
      detailsAreVisible: false,
      //   friendIsFavorite: this.friend.isFavorite,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      //   this.friendIsFavorite = !this.friendIsFavorite;
      this.$emit("toggle-favorite-clicked", this.friend.id);
    },
  },
};
</script>

