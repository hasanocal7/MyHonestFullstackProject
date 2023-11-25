<template>
  <v-container class="fill-height">
    <v-responsive class="align-center text-center fill-height">
      <v-row>
        <v-img
          height="150"
          src="https://static-00.iconduck.com/assets.00/nestjs-icon-2048x2038-6bjnpydw.png"
        />
        <v-img
          height="150"
          src="https://www.svgrepo.com/show/306946/vuetify.svg"
        />
      </v-row>

      <div class="py-7" />

      <div
        :style="{ color: fontColor }"
        class="text-body-2 font-weight-bold mb-n1"
      >
        Welcome to
      </div>

      <h1 :style="{ color: fontColor }" class="text-h2 font-weight-bold">
        Honest Project
      </h1>
      <div class="py-7" />

      <v-btn size="x-large" @click="alertBig()">User Services</v-btn>
    </v-responsive>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      fontColor: "white",
    };
  },
  methods: {
    alertBig() {
      alert("Under Construction");
    },
  },
};
</script>
