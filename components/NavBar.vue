<template>
  <div>
    <b-navbar toggleable="lg" class="nav-custom">
      <b-navbar-brand href="/">Product</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/create">Create</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <!-- <b-nav-form>
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Search"
            ></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" type="submit"
              >Search</b-button
            >
          </b-nav-form> -->

          <!-- <b-nav-item-dropdown text="Lang" right>
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href="#">ES</b-dropdown-item>
            <b-dropdown-item href="#">RU</b-dropdown-item>
            <b-dropdown-item href="#">FA</b-dropdown-item>
          </b-nav-item-dropdown> -->

          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em :style="{ color: `#3366ff` }">
                <img src="~/assets/svg/man.svg" /> {{ email }}
              </em>
            </template>
            <!-- <b-dropdown-item href="#">Profile</b-dropdown-item> -->
            <b-dropdown-item @click="logout()">
              <div :style="{ color: `red` }">
                <img src="~/assets/svg/logout.svg" /> Sign Out
              </div>
            </b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  props: {
    email: String
  },
  methods: {
    async logout() {
      console.log(`logout`);

      const auth = this.$fire.auth;
      await auth
        .signOut()
        .then(() => {
          alert("✈️ Sign-out successful.");
          this.$router.push({ path: `/login` });
        })
        .catch(error => {
          alert("🚀 error", error);
        });
    }
  }
};
</script>

<style>
.nav-custom {
  background-color: #ebf5fb;
  margin-bottom: 20px;
  border-radius: 8px;
}
</style>
