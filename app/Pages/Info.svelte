<script lang="typescript">
  import Goal from "./Goal.svelte"
  import {navigate} from "svelte-native"
  import axios from 'axios/dist/axios';

  let username: string;
  let password: string;

  const handleRegister = async () => {
    const user = {username,password}
    const response = await axios.post("https://us-central1-final-project-backend-16738.cloudfunctions.net/app/users", )
    navigate({page : Goal})
  }
</script>

<page >
  <actionBar class="action-bar"/>
  <gridLayout rows="*, auto, auto, auto" class="layout">
    <stackLayout row="0">
    <label class="title" fontSize="35" color="white" text="How does it work?" horizontalAlignment="center" fontWeight="bold"/>
    <stackLayout />
    <stackLayout row="1" class="bullet-points">
    <label class="label" fontSize="28" color="white" text=" 🏆  Create a goal" />
    <label class="label" fontSize="28" color="white" text=" 📚  Choose a category" />
    <label class="label" fontSize="28" color="white" text=" 🥂  Invite your friends" />
    <label class="label" fontSize="28" color="white" text=" 📊  Post updates and track everyones progress" textWrap="true"/> 
   </stackLayout>
    <stackLayout />
    <stackLayout row="2" class="form">
    <textField
      class="input input-border"
      hint="Username"
      keyboardType="username"
      autocorrect="false"
      autocapitalizationType="none"
      fontSize="25"
      color="white"
      textFieldHintColor="white"
      bind:text="{username}"
    />
    <textField 
      class="input input-border" 
      color="white" secure="true" 
      hint="Password" fontSize="25" 
      bind:text="{password}" 
    />
    <button text="Register" on:tap="{handleRegister}" class="button" >
  </stackLayout>
  </gridLayout>
</page>

<style>
  .layout {
    background-image: url("~/Images/Timber.jpg");
    background-position: left;
  }
  .action-bar {
    opacity: 0;
  }

  .label {
    padding: 8;
    margin-left: 20;
    font-size: 20px;
  }

  .form {
  margin-left: 30;
  margin-right: 30;
  margin-top: 50;
}

.title {
  margin-bottom: 90;
  margin-top: 50;
}

.button {
  display: inline-block;
  background-color: white;
  color: black;
  text-align: center;
  font-size: 28px;
  border-radius: 60px;
}

</style>

