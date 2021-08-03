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

</style>

<page >
    <stackLayout>
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
                <stackLayout backgroundColor="#92CD92" class="m-x-auto" >
                    <label  class="text-left header" text="GoalPage" fontSize="20"/>
                    <gridLayout columns="1*, *" class="progressbar">
                        <stackLayout text="30" col="0" class="progressbar-value"></stackLayout>
                      </gridLayout>
                      
                      <button on:tap="{() => {openModal()}}"text="Post"></button>
                      
                    <listView margin="10" backgroundColor="#E9FDE3"items="{updates}"> 
                    <Template let:item>
                        <stackLayout >
                            <gridLayout columns="50, 50" rows="*, *">
                                <image  col="0" row="0" class="-thumb img-circle" src="{item.profilePic}" />
                                <label fontWeight="bold" col="1" row="0" text="{item.user}" />
                            </gridLayout>
                            <stackLayout height="300">
                                <label col="0" row="1" class="text-left" text="{item.post}" />
                                <scrollView orientation="horizontal">
                                    <stackLayout orientation="horizontal">
                                        <image src="{item.picture}"/>
                                        <image src="{item.picture}"/>
                                        <image src="{item.picture}"/>
                                    </stackLayout>
                                </scrollView>
                            </stackLayout>
                            <button on:tap={() => navigate({ page: Comments })} text="View comments" />
                            
                        </stackLayout>
                    </Template>
                    </listView>
                </stackLayout>
            </tabContentItem>
            <tabContentItem >
                <listView margin="10" backgroundColor="#E9FDE3" items="{users}">
                    <Template let:item>
                        <stackLayout >
                            <gridLayout columns="50, 50" rows="*, *">
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
                                  <button text="progress bar"/>
                            </stackLayout>
                        </stackLayout>

                    </Template>
                </listView>

            </tabContentItem>
        </bottomNavigation>
        </stackLayout>
</page>