<template>
  <b-container class="bv-example-row" fluid="md">
    <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else>
      <div v-for="row of girls" :key="row.index">
        <b-row>
          <b-col v-for="girl of row" :key="girl[0]">
            <Card
              :id="girl[0]"
              :name="girl[1].name"
              :facebook="girl[1].facebook"
              :instrgram="girl[1].instrgram"
              :description="girl[1].description"
              :age="girl[1].age"
              :url="girl[1].url"
              :date="girl[1].date"
          /></b-col>
        </b-row>
      </div>
    </div>
  </b-container>
</template>

<script>
import { GirlsStore } from "@/store";
import { mapGetters } from "vuex";
export default {
  data() {
    return {};
  },
  async fetch() {
    await GirlsStore.getGirls();
  },
  computed: {
    girls: () => {
      let girlsArray = [];
      if (!GirlsStore.girls) return; // if empty
      const arr = Object.entries(GirlsStore.girls);
      while (arr.length) girlsArray.push(arr.splice(0, 3));
      return girlsArray;
    }
  }
};
</script>
