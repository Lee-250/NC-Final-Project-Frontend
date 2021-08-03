<script lang="typescript">
import { text } from "svelte/internal";

const { closeModal }=require("svelte-native");

const items = ["1 mile", "2 miles", "3 miles", "4 miles", "5 miles", "6 miles", "7 miles", "8 miles", "9 miles", "10 miles", "11 miles", "12 miles", "13 miles", "14 miles", "15 miles", "16 miles", "17 miles", "18 miles", "19 miles", "20 miles", "21 miles", "22 miles", "23 miles", "24 miles", "25 miles", "26 miles", "27 miles", "28 miles", "29 miles", "30 miles"]

export let userPost;


let textFromUser = '';
const addUpdate = (textFromUser):void => {
   
    userPost = {user: 'Lee', post: textFromUser, profilePic: "~/Images/blankProfilePic.png",
        picture: 'https://ftw.usatoday.com/wp-content/uploads/sites/90/2019/09/crying-cyclist.jpg?w=1000&h=576&crop=1'};
   
    closeModal(userPost);
    
}



</script>
<style>
    stackLayout {
        padding: 30;
    }

    label {
        font-size: 25;
        text-align: center;
    }

</style>

<page>
    <stackLayout class="nt-input" flexDirection="column">
    <label text="Create a post" class="font-weight-bold m-b-5" textAlign="center" />
    <textField hint="post an update" class="-border" bind:text="{textFromUser}"></textField>
    <stackLayout />
    <stackLayout class="nt-input" flexDirection="column">
    <label text="Update your progress!" class="font-weight-bold m-b-5" textAlign="center" />
    <listPicker items="{items}" class="picker"></listPicker>

    <button on:tap={() => addUpdate(textFromUser)} text="Submit" class="-primary"></button>
    </stackLayout>
</page>









