<script lang="typescript"> 

import { BottomNavigation, StackLayout, TabStripItem } from '@nativescript/core';
import { dateProperty } from '@nativescript/core/ui/date-picker';
import {navigate} from "svelte-native";
import axios from 'axios/dist/axios';
import { onMount } from 'svelte';
import {Template} from 'svelte-native/components';
import {showModal} from 'svelte-native';
import PostModal from './PostModal.svelte';
import { itemHeightProperty } from '@nativescript/core/ui/layouts/wrap-layout';
import CommentModal from './CommentModal.svelte';
import Comments from './Comments.svelte'




// { user: string, post: string, profilePic: string, picture: string }[] 

let updates  = [
        { user: 'Lee', post: 'Just got back from a 450 mile ride, too easy',
            profilePic: "~/Images/blankProfilePic.png",
            picture: 'https://ftw.usatoday.com/wp-content/uploads/sites/90/2019/09/crying-cyclist.jpg?w=1000&h=576&crop=1'},

         {user: 'Harry', post: 'I love bikes me', profilePic: "~/Images/blankProfilePic.png", picture: 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Floyd-landis-toctt.jpg/1200px-Floyd-landis-toctt.jpg'}, 

         {user: 'Chris', post: 'Quick 5 miles', profilePic: "~/Images/blankProfilePic.png", picture: 'https://cdn.road.cc/sites/default/files/styles/main_width/public/irb1oxnwkljulmqul-ya1wpvbi5z3kjnoawnpi-kk-2048x1536.jpg' },
         
         {user: 'John', post: 'Big ride planned this weekend!!', profilePic: "~/Images/blankProfilePic.png", picture: 'https://media2.fdncms.com/sevendaysvt/imager/u/original/21581403/sports1-1-b8504bdcfa56c38a.jpg'}]


let users = [{user: 'Lee', profilePic: "~/Images/blankProfilePic.png", milesCompletedThisWeek: 20, totalMilesCompleted: 50, weekStreak: 2, percentComplete: 50}, {user: 'Harry', profilePic: "~/Images/blankProfilePic.png", milesCompletedThisWeek: 25, totalMilesCompleted: 55, weekStreak: 2, percentComplete: 30}, {user: 'Chris', profilePic: "~/Images/blankProfilePic.png", milesCompletedThisWeek: 10, totalMilesCompleted: 40, weekStreak: 2, percentComplete: 20}, {user: 'John', profilePic: "~/Images/blankProfilePic.png", milesCompletedThisWeek: 15, totalMilesCompleted: 45, weekStreak: 2, percentComplete: 70}]

//  const testApi = axios.create({baseURL: "https://mygames-api.herokuapp.com/api"});

 const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app"})


 async function openModal() {
    let userPost = {};
    let result:any  = await showModal({
            page: PostModal,
            props: { userPost: userPost },
        });
        updates = [result, ...updates];
    
}
 

// onMount(async () => {
    
//         const {data}  = await devApi.get('/feed')
//         feed = data;
   
// })
const setProgressBarWidth = (percent) => {
     let columnStr = '';
    columnStr = percent + "*," + (100 - percent) + "*";
    return columnStr;
 }

</script>


<page >
    <actionBar title="Achieve" flat="true">
        <actionItem on:tap="{openModal}"
		ios.systemIcon="9" ios.position="right"
		android.systemIcon="ic_menu_share" android.position="actionBar" />
    </actionBar>
    <stackLayout >
        <bottomNavigation>
            <tabStrip>
                <tabStripItem>
                    <label text="Home" />
                </tabStripItem>
                <tabStripItem>
                    <label text="Progress" />
                </tabStripItem>
            </tabStrip>
            <tabContentItem >
                <stackLayout >
                    <stackLayout >
                      <button on:tap="{() => {openModal()}}"text="Post" class="button-post">
                    </stackLayout>
                    <listView separatorColor="white" items="{updates}" > 
                    <Template let:item>
                        <stackLayout >
                            <gridLayout columns="57, auto, *" rows="*, *" backgroundColor="white" class="grid">
                                <image  col="0" row="0" class="img" src="{item.profilePic}" />
                                <label fontWeight="bold" col="1" row="0" text="{item.user}:" fontSize="20"
                                horizontalAlignment="left" />
                                <label col="2" row="0" text="{item.post}" fontSize="20"
                                textWrap="true" />
                            </gridLayout>
                            <stackLayout height="300" >
                                <scrollView orientation="horizontal">
                                    <stackLayout orientation="horizontal" >
                                        <image src="{item.picture}"/>
                                        <image src="{item.picture}"/>
                                        <image src="{item.picture}"/>
                                    </stackLayout>
                                </scrollView>
                            </stackLayout>
                            <stackLayout class="form">
                            <button on:tap={() => navigate({ page: Comments })} text="Comments" class="button-comments"/>
                            </stackLayout>
                        </stackLayout>
                    </Template>
                    </listView>
                </stackLayout>
            </tabContentItem>
            <tabContentItem class="layout">
                <listView margin="10" items="{users}">
                    <Template let:item>
                        <stackLayout >
                            <gridLayout columns="50, 50" rows="*, *" >
                                <image  col="0" row="0" class="-thumb img-circle" src="{item.profilePic}" />
                                <label fontWeight="bold" col="1" row="0" text="{item.user}" />
                            </gridLayout>
                            <stackLayout height="300">
                                <label text="Miles completed this week: {item.milesCompletedThisWeek}"/>
                                <label text="Total miles completed: {item.totalMilesCompleted}"/>
                                <label text="Week streak: {item.weekStreak}" />
                                <gridLayout columns="{setProgressBarWidth(item.percentComplete)}" class="progressbar">
                                    <stackLayout col="0" class="progressbar-value"></stackLayout>
                                  </gridLayout>
                            </stackLayout>
                        </stackLayout>

                    </Template>
                </listView>

            </tabContentItem>
        </bottomNavigation>
        </stackLayout>
</page>

<style>

.progressbar {
        height: 20;
        margin: 10;
        border-radius: 10;
        border-color: black;
        border-width: 1;
    }
.progressbar-value {
        background: #337ab7;
        border-radius: 10;
    
    }

.button-post {
    background-color: white;
    border-color: black;
    color: black;
    text-align: center;
    font-size: 28px;
    border-radius: 50%;
    position: center;
    width: 280;
    margin-top: 30;
  }
  .button-comments {
    background-color: rgb(99, 54, 232);
    color: black;
    text-align: center;
    font-size: 16px;
    border-radius: 50%;
    margin-left: 210;
    width: 140;
  }
  .form {
  margin-left: 5;
  margin-right: 5;  
}

.img {
    border-radius: 40%;
}

.grid {
    border-radius: 40%;
}

</style>