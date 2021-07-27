<script lang="typescript">
  import Start from "./Pages/Start.svelte";

  import { navigate } from "svelte-native";

  let message: string = "Blank Svelte Native App";
</script>

<page>
  <stackLayout paddingBottom="80">
    <label
      text="Achieve"
      fontSize="70"
      horizontalAlignment="center"
      color="white"
    />
    <image src="~/Images/trophy.png" />
    <button on:tap={() => navigate({ page: Start })} text="Start" />
  </stackLayout>
</page>

<style>
</style>
