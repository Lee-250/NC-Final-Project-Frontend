<script lang="typescript">
    import axios from 'axios/dist/axios';

    const { closeModal }=require("svelte-native");

    export let loggedInUser;
    export let users;
    export let feed;

    let textFromUser = '';
    const addUpdate = async (textFromUser): Promise<void> => {
        let post = {
            user: 'Lee', 
            postBody: textFromUser,
            avatar: "https://i.imgur.com/DSuXVcf.jpg",
            imageURL: imageURL
        }
        const response = await axios.put("https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/tJgU7tw7OYIlQ88spYlt/feed", post)
        closeModal();
    }
    let imageURL = ''

    const sendImageURL = () => {
        imageURL = "https://www.ride25.com/wp-content/uploads/2014/03/tired-racer-ride-25.jpg";
        console.log(imageURL);
    }

    let value = 0;
</script>

<style>
    stackLayout {
        padding: 20;
    }

    label {
        font-size: 25;
        text-align: center;
    }

    .post-background {
        background-image: url("~/Images/Timber.jpg");
    }
    .content-background {
            background-color: honeydew;
            border: 5;
            margin: 5px;
            border-radius: 5;
        }

    .post-buttons {
        background-color: honeydew;
        border-radius: 5;
    }     
</style>

<page>
    <stackLayout  class="post-background" flexDirection="column">
        <stackLayout class="content-background">

    <label text="Create a post" textAlign="center" />
    <textField hint="post an update" class="-border" bind:text="{textFromUser}"></textField>
    <label text="Post a picture"   />
    <stackLayout  height="250" >
        <scrollView orientation="horizontal">
            <stackLayout orientation="horizontal" >
                
                    <image src="https://i.guim.co.uk/img/media/3b985a7e7023d27de64cf7b0307e3c47e23d5d0b/800_492_3646_2187/master/3646.jpg?width=445&quality=45&auto=format&fit=max&dpr=2&s=acf1c4feefa6ef880fe497e8c3258700"/>
                    <stackLayout></stackLayout>
                    <image src="https://www.ride25.com/wp-content/uploads/2014/03/tired-racer-ride-25.jpg"/>
                    <stackLayout></stackLayout>
                    <image src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSC7MYEGTlm5cxtWNfIAn7WJL1635u4pmmZUzZVTnHRBYT6_xHatIsqwKvpdHX1alMVKoU&usqp=CAU"/>
            </stackLayout> 
        </scrollView>
    </stackLayout>
    
    <stackLayout>
        <button on:tap={() => sendImageURL()} text="Select Photo" />
    </stackLayout>
    <stackLayout  flexDirection="column">
        <label text="Miles completed"  textAlign="center" />
        <slider minValue=0 maxValue=30 bind:value="{value}" />
        <label text="{Math.floor(value) }" />
        <button on:tap={() => {
                addUpdate(textFromUser)
            }} text="Submit" >
        </button>
    </stackLayout>
    </stackLayout>
</page>









