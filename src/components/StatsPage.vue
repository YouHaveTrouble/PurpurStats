<template>
  <section v-if="!errored" class="statsPage">
    <p>
      <span>There are currently</span>
      <span class="amount">{{ versionCounts[chosenVersion] }}</span>
      <span>Purpur servers on <select name="versions" v-model="chosenVersion">
      <option v-for="version in versions" :key="version">{{version}}</option>
    </select></span></p>
  </section>
  <section v-else>
    <p>An error occured while loading data. Try again later!</p>
  </section>
</template>

<script>
export default {
  name: "StatsPage",
  data() {
    return {
      versions: [],
      versionCounts: {},
      chosenVersion: "",
      errored: false,
    }
  },
  async mounted() {
    let purpurVersions = await fetch("https://bstats.org/api/v1/plugins/5103/charts/minecraft_version/data");
    if (purpurVersions.status !== 200) {
      this.errored = true;
      return;
    }
    const json = await purpurVersions.json();
    for (const entry in json) {
      this.versions.push(json[entry].name);
      this.versionCounts[json[entry].name] = json[entry].y;
    }

    this.versions = this.versions.map( a => a.split('.').map( n => +n+100000 ).join('.') ).sort()
        .map( a => a.split('.').map( n => +n-100000 ).join('.') );

    this.chosenVersion = this.versions[this.versions.length-1];
  }
}
</script>

<style scoped>
p {
  break-inside: avoid-column;
  font-size: 1.2rem;
}

select {
  font-size: 2rem;
}

.amount {
  font-size: 2rem;
}

.amount::before,
.amount::after {
  content: " ";
}
</style>