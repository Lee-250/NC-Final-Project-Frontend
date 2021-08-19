<script lang="typescript">
  import { navigate } from "svelte-native";
  import SetupComplete from "./SetupComplete.svelte"

  let someDate: Date;
  let goalTitle: string;
  let selectedCategory: string;
  let goalMiles: number;

  const items = ["Health", "Fitness", "Skill", "Social", "Career"] 
 
  const handleSubmit = async () =>{
    navigate({page : SetupComplete});
  }
</script>

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
    font-size: 20px;
    border-radius: 50%;
    position: center;
    margin-top: 20;
    margin-left: 60;
    margin-right: 60;
  }
</style>

<page>
  <scrollView>
    <stackLayout class="layout">
      <stackLayout>
        <label text="Select a category"  
          fontSize="30"
          horizontalAlignment="center"
          class="label"
          color="white"
          fontWeight="bold">
        </label>
        <listPicker items="{items}" 
          class="picker"
          bind:selectedIndex={selectedCategory}>
        </listPicker>
        <label text="Select an activity" 
          fontSize="30"
          horizontalAlignment="center"
          class="label"
          color="white"
          fontWeight="bold">
        </label>
        <textField hint="e.g. Cycling, running" 
          fontSize="20"
          horizontalAlignment="center"
          color="white"
          bind:text="{goalTitle}">
        </textField>
        <label text="Miles per week?" 
          fontSize="30"
          horizontalAlignment="center"
          class="label"
          color="white"
          fontWeight="bold">
        </label>
        <textField hint="e.g. 30" 
          fontSize="20"
          horizontalAlignment="center"
          color="white"
          bind:text="{goalTitle}">
        </textField>
        <label text="Completion date" 
          fontSize="30"
          horizontalAlignment="center"
          class="label"
          color="white"
          fontWeight="bold">
        </label>
        <datePicker class="date-picker" bind:date="{someDate}"></datePicker>
        <button text="Submit" on:tap="{handleSubmit}" class="button"></button>
      </stackLayout>
    </stackLayout>
  </scrollView>
</page>
