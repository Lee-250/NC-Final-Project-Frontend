<script lang="typescript">
    import Goal from "./Goal.svelte"
    import {navigate} from "svelte-native"



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
    <label class="label" fontSize="28" color="white" text=" 📊  Post updates and track
        everyones progress" textWrap="true"/> 
   </stackLayout>
    <stackLayout />
    <stackLayout row="2" class="form">
    <textField
      class="input input-border"
      hint="Email"
      keyboardType="email"
      autocorrect="false"
      autocapitalizationType="none"
      fontSize="25"
      color="white"
      textFieldHintColor="white"
    />
    <textField class="input input-border" color="white" secure="true" hint="Password" fontSize="25" />
    <button text="Register" on:tap="{()=> navigate({page : Goal})}" class="button" >
  </stackLayout>
  </gridLayout>
</page>

<style>
  .layout {
    background-image: url("~/Images/Timber.jpg");
    background-position: center;
  }
  .action-bar {
    opacity: 0;
  }

  .label {
    padding: 15;
    margin-left: 20;
  }

  .form {
  margin-left: 30;
  margin-right: 30;
  margin-top: 90;
  flex-grow: 2;  
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

