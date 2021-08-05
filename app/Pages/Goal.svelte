<script lang="typescript">
  import { navigate } from "svelte-native";
  import SetupComplete from "./SetupComplete.svelte"
  import axios from 'axios/dist/axios';

  let someDate: Date;
  let goalTitle: string;
  let selectedCategory: string;

  const items = ["Health", "Fitness", "Skill", "Social", "Career"] 
 
  const handleSubmit = async () =>{
    const goal = {
      goalName: goalTitle,
      goalTarget: 50,
      category: items[selectedCategory],
      endDate: someDate,
    }
    const response = await axios.post("https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals", goal)
    navigate({page : SetupComplete});
  }
</script>

<page>
  <scrollView>

    <stackLayout class="layout">
      <stackLayout  >
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
          <!-- <gridLayout horizontalAlignment="center" columns="80, 80, 80, 80" rows="50, 10">
             <label text="0,0" row="0" col="0" backgroundColor="#4383b8"/> -->
            
              <!-- <image row="0" col="0" src="font://&#xf206;" class="fas fa-bicycle" />
              <label horizontalAlignment="center" row="1" col="0" text="Fitness" /> -->
            
            <!-- <label text="0,1" row="0" col="1" backgroundColor="#1c486b"/> -->
            
              <!-- <image row="0" col="1"  src="font://&#xf140;" class="fas fa=bullseye" />
              <label horizontalAlignment="center" row="1" col="1"  text="Skill" /> -->
            
            <!-- <label text="1,0" row="1" col="0" backgroundColor="#286290"/> -->
            
              <!-- <image row="0" col="2" src="font://&#xf0c0;" class="fas fa-users" />
              <label horizontalAlignment="center" row="1" col="2"  text="Social" />
             -->
            <!-- <label text="1,1" row="1" col="1" backgroundColor="#4383b8"/> -->
            
              <!-- <image row="0" col="3"  src="font://&#xf0f0" class="fas fa-user-md" />
              <label horizontalAlignment="center" row="1" col="3"  text="Career"/> -->

            
          <!-- </gridLayout> --> -->
          <listPicker items="{items}" class="picker"
            bind:selectedIndex={selectedCategory}></listPicker>
            <label text="Select an activity" fontSize="30"
            horizontalAlignment="center"
            class="label"
            color="white"
            fontWeight="bold"></label>
            <textField hint="e.g. Cycling, running" fontSize="20"
            horizontalAlignment="center"
            color="white"
            bind:text="{goalTitle}"></textField>
            <label text="How many miles per week?" fontSize="30"
            horizontalAlignment="center"
            class="label"
            color="white"
            fontWeight="bold"></label>
            <textField hint="e.g. 30" fontSize="20"
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
      </scrollView>
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