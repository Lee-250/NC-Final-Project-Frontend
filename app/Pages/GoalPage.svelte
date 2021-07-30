<script lang="typescript"> 

import { BottomNavigation, StackLayout, TabStripItem } from '@nativescript/core';
import { dateProperty } from '@nativescript/core/ui/date-picker';
import axios from 'axios/dist/axios';
import { onMount } from 'svelte';
import {Template} from 'svelte-native/components';
import {showModal} from 'svelte-native';
import ModalPage from './ModalPage.svelte';

let updates: { user: string, post: string, profilePic: string, picture: string }[] = [{
         user: 'Lee', 
         post: 'Just got back from a 450 mile ride, too easy', 
        profilePic: "~/Images/blankProfilePic.png",
        picture: 'https://ftw.usatoday.com/wp-content/uploads/sites/90/2019/09/crying-cyclist.jpg?w=1000&h=576&crop=1'},
         {user: 'Harry', post: 'I love bikes me', profilePic: "~/Images/blankProfilePic.png", picture: 'https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Floyd-landis-toctt.jpg/1200px-Floyd-landis-toctt.jpg'}, {user: 'Chris', post: 'Quick 5 miles', profilePic: "~/Images/blankProfilePic.png", picture: 'https://cdn.road.cc/sites/default/files/styles/main_width/public/irb1oxnwkljulmqul-ya1wpvbi5z3kjnoawnpi-kk-2048x1536.jpg' },{user: 'John', post: 'Big ride planned this weekend!!', profilePic: "~/Images/blankProfilePic.png", picture: 'https://media2.fdncms.com/sevendaysvt/imager/u/original/21581403/sports1-1-b8504bdcfa56c38a.jpg'}]

 let newPost: { user: string, post: string } = {user: 'Lee', post: ''};

//  const testApi = axios.create({baseURL: "https://mygames-api.herokuapp.com/api"});

 const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app"})

let feed = [];

 onMount(async () => {
     
         const {data}  = await devApi.get('/feed')
         feed = data;
    
})

async function openModal() {
    await showModal({page: ModalPage});
  }






 const addUpdate = ():void => {
    updates = [{user: newPost.user, post: newPost.post}, ...updates];
    newPost.post = '';
    
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
                    <gridLayout columns="3*, *" class="progressbar">
                        <stackLayout col="0" class="progressbar-value"></stackLayout>
                      </gridLayout>
                      <button on:tap="{openModal}"text="Post"></button>
                    <listView margin="10" backgroundColor="#E9FDE3"items="{updates}"> 
                    <Template let:item>
                        <stackLayout >
                            <gridLayout columns="50, 50" rows="*, *">
                                <image  col="0" row="0" class="-thumb img-circle" src="{item.profilePic}" />
                                <label fontWeight="bold" col="1" row="0" text="{item.user}" />
                            </gridLayout>
                            <stackLayout height="300">
                                <label col="0" row="1" class="text-left" text="{item.post}" />
                                <image src="{item.picture}"/>
                            </stackLayout>
                        </stackLayout>
                    </Template>
                    </listView>
                </stackLayout>
            </tabContentItem>
            <tabContentItem>
                <label text="progress" />
            </tabContentItem>
        </bottomNavigation>
        </stackLayout>
</page>