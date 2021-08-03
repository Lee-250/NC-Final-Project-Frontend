<script lang="typescript">
import Info from "./Info.svelte";
import {navigate} from "svelte-native";
import GoalPage from "./GoalPage.svelte";
</script>

<page>
    <stackLayout class="layout">
        <stackLayout class="form">
            <label text="First time here?" fontSize="40"
            horizontalAlignment="center"
            color="white"
            class="title1"
            fontWeight="bold"></label>
            <button on:tap="{() =>navigate({page: Info})}" text="Setup" class="button"></button>
            </stackLayout>
            <label text="Returning user" fontSize="40"
            horizontalAlignment="center"
            color="white"
            class="title2"
            fontWeight="bold"></label>
            <stackLayout class="form">
            <textField class="input input-border" hint="Email" keyboardType="email"
            autocorrect="false"
            autocapitalizationType="none"
            fontSize="25"
            color="white"
            textFieldHintColor="white"></textField>
            <textField class="input input-border" hint="Username" keyboardType="email"
            autocorrect="false"
            autocapitalizationType="none"
            fontSize="25"
            color="white"
            textFieldHintColor="white"></textField>
            <textField class="input input-border" color="white" secure="true" hint="Password" fontSize="25"></textField>
            <button on:tap={() => navigate({ page: GoalPage })} text="Login" class="button"></button>
        </stackLayout>
    </stackLayout>
</page>


<style>

.layout {
        background-image: url("~/Images/Timber.jpg");
        background-position: center;
      }

.title1 {
    margin-top: 100;
    margin-bottom: 12;
  }

.title2 {
    margin-top: 80;
    margin-bottom: 20;
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

.form {
  margin-left: 40;
  margin-right: 40;
  flex-grow: 2;  
  margin-bottom: 60;
}

</style>