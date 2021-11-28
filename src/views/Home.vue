<template>
  <div class="home">
    <HelloWorld msg="Temper Onboarding Flow" />
    <Chart />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import Chart from "@/components/Chart.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
    Chart,
  },
};
</script>
