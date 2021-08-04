<script lang="typescript">
  import { navigate } from "svelte-native";
  import SetupComplete from "./SetupComplete.svelte"
  import axios from 'axios/dist/axios';

  let someDate: Date;
  let goalTitle: string;
  let selectedCategory: string;

  const items = ["Health", "Fitness", "Skill", "Social", "Career"] 
  const goal = {
	goalName: goalTitle,
	goalTarget: 50,
	category: selectedCategory,
  endDate: someDate,
}
  const handleSubmit = async () =>{
    const response = await axios.post("https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals", goal)
    navigate({page : SetupComplete});
  }
</script>

<page>
  <stackLayout class="layout">new Date()
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
      <listPicker items="{items}" class="picker"
      bind:selectedIndex={selectedCategory}></listPicker>
    <label text="What is your goal?" fontSize="30"
    horizontalAlignment="center"
    class="label"
    color="white"
    fontWeight="bold"></label>
      <textField hint="eg. cycle 30 miles per week" fontSize="20"
      horizontalAlignment="center"
      color="white"
      bind:text="{goalTitle}"></textField>
    <label text="Completion date" fontSize="30"
    horizontalAlignment="center"
    class="label"
    color="white"
    fontWeight="bold"></label>
    <datePicker class="date-picker" bind:date="{someDate}"></datePicker>
    <button text="Submit" on:tap="{handleSubmit}" class="button"></button>
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
        background-position: left;
      }
/* .title {
  margin-top: 40;
} */
.form {
  margin-left: 40;
  margin-right: 40;
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