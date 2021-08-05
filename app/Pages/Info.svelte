<script lang="typescript">
  import Goal from "./Goal.svelte";
  import { navigate } from "svelte-native";
  import axios from "axios/dist/axios";
  import { GridLayout } from "@nativescript/core";

  let username: string;
  let password: string;

  const handleRegister = async () => {
    const user = { username, password };
    const response = await axios.post(
      "https://us-central1-final-project-backend-16738.cloudfunctions.net/app/users"
    );
    navigate({ page: Goal });
  };
</script>

<page>
  <actionBar class="action-bar" />
  <stackLayout columns="2" rows="4" class="layout">
    <stackLayout row="0">
      <label
        class="title"
        fontSize="35"
        color="white"
        text="How does it work?"
        horizontalAlignment="center"
        fontWeight="bold"
      />
      <stackLayout />
      <gridLayout columns="50, 325" rows="50, 50, 50, 50" class="bullet-points">
        <image row="0" col="0" src="font://&#xf091;" class="fas fa-trophy" />
        <label
          row="0"
          col="1"
          class="label"
          fontSize="28"
          color="white"
          text="Create a goal"
        />
        <image row="1" col="0" src="font://&#xf24d;" class="fas fa-clone" />
        <label
          row="1"
          col="1"
          class="label"
          fontSize="28"
          color="white"
          text="Choose a category"
        />
        <image
          row="2"
          col="0"
          src="font://&#xf500;"
          class="fas fa-user-friends"
        />
        <label
          row="2"
          col="1"
          class="label"
          fontSize="28"
          color="white"
          text="Invite your friends"
        />
        <image row="3" col="0" src="font://&#xf044;" class="fas fa-edit" />
        <label
          row="3"
          col="1"
          class="label"
          fontSize="28"
          color="white"
          text="Post updates and track everyones progress"
          textWrap="true"
        />
      </gridLayout>
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
          bind:text={username}
        />
        <textField
          class="input input-border"
          color="white"
          secure="true"
          hint="Password"
          fontSize="25"
          bind:text={password}
        />
        <button
          text="Register"
          on:tap={handleRegister}
          class="button"
        /></stackLayout
      >
    </stackLayout></stackLayout
  >
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
    margin-left: 10;
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

  .fas {
    margin: 0;
    margin-left: 25;
    padding: 0;
    width: 30;
    color: white;
  }
</style>
