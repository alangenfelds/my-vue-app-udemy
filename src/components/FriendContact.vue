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
    <button @click="$emit('delete-contact', friend.id)">Delete</button>
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
  emits: ["toggle-favorite-clicked", "delete-contact"],
  //   emits: {
  //     "toggle-favorite-clicked": (id) => {
  //       if (id) {
  //         return true;
  //       } else {
  //         console.warn("Friend ID was not provided during emit");
  //         return false;
  //       }
  //     },
  //   },
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
    // deleteContact() {
    //   this.$emit("delete-contact", this.friend.id);
    // },
  },
};
</script>

