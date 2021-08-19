<script lang="typescript">
  import {navigate} from "svelte-native";
  import GoalPage from "./GoalPage.svelte";
</script>

<page>
  <stackLayout class="layout">
    <stackLayout class="form">
      <label
        fontSize="40"
        color="white"
        text="You just set up your first goal!"
        textWrap="true"
        fontWeight="bold"
        class="label2"/>
      <label fontSize="40" color="white" text="Good luck!" fontWeight="bold" class="label"/>
      <label
        fontSize="40"
        color="white"
        text="'Winners never quit, and quitters never win!'"
        textWrap="true"
        fontStyle="italic"
        class="label"/>
      <button on:tap={() => navigate({ page: GoalPage })} text="Continue" class="btn"/>
    </stackLayout>
  </stackLayout>
</page>

<style>
  .layout {
    background-image: url("~/Images/Timber.jpg");
    background-position: left;
  }
  .form {
    margin-left: 30;
    margin-right: 30;
    margin-top: 50;
  }
  .btn {
    background-color: rgb(255, 255, 255);
    color: black;
    text-align: center;
    font-size: 20px;
    border-radius: 50%;
    margin-left: 40;
    margin-right: 40;
  }
  .label {
    padding: 8;
    text-align: center;
    margin-bottom: 75;
  }
  .label2 {
    padding: 8;
    text-align: center;
    margin-bottom: 20;
    margin-top: 40;
  }
</style>
