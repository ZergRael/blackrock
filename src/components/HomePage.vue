<template>
  <h1 class="text-xl block text-center">Blackrock Analyzer</h1>
  <div class="home-page">
    <table>
      <thead>
        <tr>
          <th></th>
          <th v-for="f in fights" :key="f.id">{{ f.name }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="a in actors" :key="a.id">
          <td>{{ a.name }}</td>
          <Cell
            v-for="f in fights"
            :key="f.id"
            :fight="f"
            :buffs="a.fights.find((e) => e.id == f.id)"
          />
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import Cell from "@/components/Cell";

export default {
  name: "HomePage",
  components: {
    Cell,
  },
  data() {
    return {
      fights: [],
      actors: [],
    };
  },
  async created() {
    const code = window.location.pathname.slice(1);
    if (!code) {
      return;
    }

    const res = await axios.get(`${process.env.VUE_APP_API_ENDPOINT}/${code}`);

    this.fights = res.data.fights;
    this.actors = res.data.actors;
  },
};
</script>
