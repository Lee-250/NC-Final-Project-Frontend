<script lang="typescript">
  import Start from "./Pages/Start.svelte";

  import { navigate } from "svelte-native";

  let message: string = "Blank Svelte Native App";
</script>

<page>
  <stackLayout paddingBottom="80" class="layout">
    <image src="~/Images/trophy3.png" class="img"/>
    <stackLayout class="form">
    <label
      text="Achieve"
      fontSize="70"
      horizontalAlignment="center"
      color="white"
      class="title"
      fontWeight="bold"
    />
    <button on:tap={() => navigate({ page: Start })} text="Start" class="button" />
    </stackLayout>
  </stackLayout>
</page>

<style>
  .layout {
    background-image: url("~/Images/Timber.jpg");
    background-position: left;
  }

  .title {
    margin-bottom: 30;
  }
  
  .button {
    background-color: white;
    color: black;
    text-align: center;
    font-size: 28px;
    border-radius: 50%;
    position: center;
  }

  .img {
    margin-top: 150;
  }

  .form {
  margin-left: 40;
  margin-right: 40;  
}

</style>
