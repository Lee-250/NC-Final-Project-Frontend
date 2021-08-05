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
let imageURL = ''

const sendImageURL = () => {
    imageURL = "https://www.ride25.com/wp-content/uploads/2014/03/tired-racer-ride-25.jpg";
    console.log(imageURL);
    
}


let value = 0;





</script>
<style>
 
    label {
        font-size: 25;
        text-align: center;
    }

    .post-background {
        background-image: url("~/Images/Timber.jpg");
        padding: 20;
    }

    .post-buttons {
        background-color: honeydew;
        border-radius: 5;
    }     
    .button {
  display: inline-block;
  background-color: white;
  color: black;
  text-align: center;
  font-size: 28px;
  border-radius: 60px;
  margin-left: 60;
  margin-right: 60;
}
.button-photo {
  display: inline-block;
  background-color: white;
  color: black;
  text-align: center;
  font-size: 28px;
  border-radius: 60px;
  margin-bottom: 70;
  margin-left: 60;
  margin-right: 60;
}
.post-update {
    background-color: white;
    border-color: black;
    border-radius: 10px;
    text-align: center;
    margin-bottom: 70;
    margin-left: 20;
}

/* .post-picture {
    margin-right: 30;
} */

</style>




<page>
    <stackLayout class="post-background" >
        <stackLayout >

        
    <label text="Create a post" textAlign="center" color="white" fontWeight="bold" fontSize="34"/>
    <textField hint="start typing" class="post-update" textFieldHintColor="white" fontSize="25" bind:text="{textFromUser}" ></textField>
    <stackLayout  height="260" >
        <!-- <label text="Post a picture" color="white" fontWeight="bold" fontSize="34" /> -->
        <scrollView orientation="horizontal" >
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
        <button on:tap={() => sendImageURL()} text="Select Photo" class="button-photo"/>
        </stackLayout>
    <stackLayout  flexDirection="column">
        <label text="Miles completed"  textAlign="center" color="white" fontWeight="bold" fontSize="34" />
        <slider minValue=0 maxValue=30 bind:value="{value}" />
        <label text="{Math.floor(value) }" color="white" fontWeight="bold" fontSize="34"/>
        <button on:tap={() => addUpdate(textFromUser)} text="Submit" class="button" />
    </stackLayout>
    </stackLayout>
</page>









