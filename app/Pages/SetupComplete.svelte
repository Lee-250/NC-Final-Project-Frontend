<script lang="typescript">
  // import Goalpage from "./Goalpage.svelte";
  import {navigate} from "svelte-native";
import GoalPage from "./GoalPage.svelte";
</script>

<page>
  <stackLayout class="layout">
    <label
      fontSize="35"
      color="white"
      text="You just set up your first goal!"
      textWrap="true"
    />
    <label fontSize="35" color="white" text="Good luck!" />

    <label
      fontSize="35"
      color="white"
      text="Winners never quit, and quitters never win!"
      textWrap="true"
    />

    <button on:tap={() => navigate({ page: GoalPage })} text="Go to Homepage" />
  </stackLayout>
</page>

<style>
  .layout {
    background-image: url("~/Images/Timber.jpg");
    background-position: center;
  }
</style>
