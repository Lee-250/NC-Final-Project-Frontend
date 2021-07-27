<script lang="typescript">
//import  from "./Pages/Start.svelte";
//import {navigate} from "svelte-native";
</script>

<style>

</style>


<page>
    <actionBar text="intro"></actionBar>
    <stackLayout>
            <label text="First time here?" fontSize="50"></label>
            <button text="Lets start"></button>
            <label text="Returning user" fontSize="50"></label>
            <textField class="input" hint="email"></textField>
            <textField class="input" hint="username"></textField>
            <textField class="input" hint="password"></textField>
            <!-- <button on:tap="{() =>navigate({page: Info})}" text="Start" ></button> -->
    </stackLayout>
</page>