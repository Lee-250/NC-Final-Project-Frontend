<script lang="typescript">
const { closeModal }=require("svelte-native");

export let userComment;

let textFromUser = '';
const addUpdate = (textFromUser):void => {
   
   userComment = {user: 'John', commentBody: textFromUser, profilePic: "~/Images/blankProfilePic.png"};
  console.log(userComment)
   closeModal(userComment);
   
}

</script>

<style>

</style>



<page>
    <stackLayout class="nt-input" flexDirection="column">
        <label text="Encourage your friends!" class="font-weight-bold m-b-5" textAlign="center" />
        <textField hint="Post a comment" class="-border" bind:text="{textFromUser}"></textField>
        <stackLayout />
        <stackLayout class="nt-input" flexDirection="column">
        <label text="Update your progress!" class="font-weight-bold m-b-5" textAlign="center" />
        
        <button on:tap={() => addUpdate(textFromUser)} text="Submit" class="-primary"></button>
        </stackLayout>
</page>