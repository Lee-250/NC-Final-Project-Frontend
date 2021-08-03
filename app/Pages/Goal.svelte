<script lang="typescript">
  import { navigate } from "svelte-native";
  import SetupComplete from "./SetupComplete.svelte"

  const items = ["Health", "Fitness", "Skill", "Social", "Career"] 
</script>

<page>
  <stackLayout class="layout">
    <stackLayout class="form">
    <!-- <label text="Create Your Goal" fontSize="40"
    horizontalAlignment="center"
    color="white"
    class="title"
    fontWeight="bold"></label> -->
    <label text="Select a category" fontSize="30"
    horizontalAlignment="center"
    class="label"
    color="white"
    fontWeight="bold"></label>
    <listPicker items="{items}" class="picker"></listPicker>
    <label text="What is your goal?" fontSize="30"
    horizontalAlignment="center"
    class="label"
    color="white"
    fontWeight="bold"></label>
    <textField hint="eg. cycle 30 miles per week" fontSize="20"
    horizontalAlignment="center"
    color="white"></textField>
    <label text="Completion date" fontSize="30"
    horizontalAlignment="center"
    class="label"
    color="white"
    fontWeight="bold"></label>
    <datePicker class="date-picker"></datePicker>
    <button text="Submit" on:tap="{()=> navigate({page : SetupComplete})}" class="button"></button>
  </stackLayout>
  </stackLayout>
</page>

<style>
  .picker {
    border-width: 2;
    background-color: white;
    border-color: white;
    border-radius: 20;
    height: 150;
    width: 325;
    vertical-align: middle;
}
.date-picker {
    background-color: white;
    border-color: white;
    border-width: 2;
    border-radius: 20;
    height: 150;
    width: 325;
    vertical-align: middle;
}
.layout {
        background-image: url("~/Images/Timber.jpg");
        background-position: center;
      }
/* .title {
  margin-top: 40;
} */
.form {
  margin-left: 40;
  margin-right: 40;
  flex-grow: 2; 
  margin-top: 22; 
}

.label {
    margin-top: 50;
    margin-bottom: 15;
  }

  .button {
    background-color: white;
    color: black;
    text-align: center;
    font-size: 28px;
    border-radius: 50%;
    position: center;
    margin-top: 20;
  }
</style>