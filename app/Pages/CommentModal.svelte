<script lang="typescript">
    import axios from 'axios/dist/axios';
    const { closeModal }=require("svelte-native");

    export let userComment;
    export let postId

    let textFromUser = '';
    const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/tJgU7tw7OYIlQ88spYlt/feed"})
    const addUpdate = async (textFromUser): Promise<void> => {
        const response = await devApi.put(`/${postId}`, {commentBody: textFromUser, username: "fred"})
        userComment = {username: 'fred', commentBody: textFromUser, profilePic: "~/Images/blankProfilePic.png"};
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