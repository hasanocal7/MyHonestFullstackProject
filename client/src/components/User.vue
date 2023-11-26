<template>
  <VContainer>
    <VResponsive>
      <VDataTable :headers="headers" :items="users">
        <template v-slot:top>
          <VToolbar flat>
            <VToolbarTitle>User API</VToolbarTitle>
            <VDivider class="mx-4" inset vertical></VDivider>
            <VSpacer></VSpacer>
            <VDialog v-model="dialog" max-width="500px">
              <template v-slot:activator="{ props }">
                <VBtn color="primary" dark class="mb-2" v-bind="props">
                  Create User
                </VBtn>
              </template>
              <VCard>
                <VCardTitle>
                  <span class="text-h5">{{ formTitle }}</span>
                </VCardTitle>

                <VCardText>
                  <VContainer>
                    <VRow>
                      <VCol cols="12" sm="6" md="4">
                        <VTextField
                          v-model="editedItem.username"
                          label="Username"
                        ></VTextField>
                      </VCol>
                      <VCol cols="12" sm="6" md="4">
                        <VTextField
                          v-model="editedItem.password"
                          label="Password"
                        ></VTextField>
                      </VCol>
                    </VRow>
                  </VContainer>
                </VCardText>

                <VCardActions>
                  <VSpacer></VSpacer>
                  <VBtn color="blue-darken-1" variant="text" @click="close">
                    Cancel
                  </VBtn>
                  <VBtn color="blue-darken-1" variant="text" @click="insert">
                    Save
                  </VBtn>
                </VCardActions>
              </VCard>
            </VDialog>
            <VDialog v-model="dialogDelete" max-width="500px">
              <VCard>
                <VCardTitle class="text-h5"
                  >Are you sure you want to delete this item?</VCardTitle
                >
                <VCardActions>
                  <VSpacer></VSpacer>
                  <VBtn
                    color="blue-darken-1"
                    variant="text"
                    @click="closeDelete"
                    >Cancel</VBtn
                  >
                  <VBtn
                    color="blue-darken-1"
                    variant="text"
                    @click="deleteItemConfirm"
                    >OK</VBtn
                  >
                  <VSpacer></VSpacer>
                </VCardActions>
              </VCard>
            </VDialog>
          </VToolbar>
        </template>
        <template v-slot:item.actions="{ item }">
          <VIcon size="small" class="me-2" @click="update(item)">
            mdi-pencil
          </VIcon>
          <VIcon size="small" @click="deleteU(item)"> mdi-delete </VIcon>
        </template>
        <template v-slot:no-data>
          <VBtn color="primary" @click="initialize"> Reset </VBtn>
        </template>
      </VDataTable>
    </VResponsive>
  </VContainer>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        title: "ID",
        align: "start",
        sortable: false,
        key: "_id",
      },
      { title: "Username", key: "username" },
      { title: "Password", key: "password" },
      { title: "Actions", key: "actions", sortable: false },
    ],
    users: [],
    editedIndex: -1,
    editedItem: {
      username: "",
      password: "",
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New User" : "Edit User";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.fetchData();
  },

  methods: {
    async fetchData() {
      try {
        const response = await axios.get("http://localhost:4000/users");
        this.users = response.data;
        console.log(this.users);
      } catch (error) {
        console.error("Veri alınamadı:", error);
      }
    },

    async update(id) {
      try {
        const response = await axios.put(
          `http://localhost:4000/users/${id}`,
          this.editedItem
        );
        console.log(response);
      } catch (error) {
        console.error("Veri güncellenemedi:", error);
      }
    },

    async update(id) {
      try {
        const response = await axios.put(
          `http://localhost:4000/users/${id}`,
          this.editedItem
        );
        console.log(response);
      } catch (error) {
        console.error("Veri güncellenemedi:", error);
      }
    },

    async deleteU(id) {
      try {
        const response = await axios.delete(
          `http://localhost:4000/users/${id}`
        );
        console.log(response);
      } catch (error) {
        console.error("Veri silinemedi:", error);
      }
    },
  },
};
</script>
