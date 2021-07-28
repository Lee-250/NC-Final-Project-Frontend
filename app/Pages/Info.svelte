<script lang="typescript">

    import Goal from "./Goal.svelte"
    import {navigate} from "svelte-native"


</script>

<page>

  <stackLayout>
    <label fontSize="35" text="How does it work?" />
    <label color="white" text="Create a goal" />
    <label color="white" text="Choose a goal category" />
    <label color="white" text="Invite your friends" />
    <label
      color="white"
      text="Encourage eachother, post updates and track your progress!"
    />
    <textField
      class="input input-border"
      hint="Email Address"
      keyboardType="email"
      autocorrect="false"
      autocapitalizationType="none"
    />
    <textField class="input input-border" secure="true" hint="Password" />
    <button text="Register" on:tap="{()=> navigate({page : Goal})}"/>
  </stackLayout>
</page>

<style>
</style>

