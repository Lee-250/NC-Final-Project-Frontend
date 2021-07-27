<script lang="typescript">
import Info from "./Info.svelte";
import {navigate} from "svelte-native";
</script>

<style>

</style>


<page>
    <actionBar text="intro"></actionBar>
    <stackLayout>
            <label text="First time here?" fontSize="50"></label>
            <button on:tap="{() =>navigate({page: Info})}" text="Lets start"></button>
            <label text="Returning user" fontSize="50"></label>
            <textField class="input" hint="email"></textField>
            <textField class="input" hint="username"></textField>
            <textField class="input" hint="password"></textField>
            <button text="Start" ></button>
    </stackLayout>
</page>