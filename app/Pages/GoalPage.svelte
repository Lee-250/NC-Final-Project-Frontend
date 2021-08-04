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
    
    
     const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/XGqXEyOP0AanWsqyRqj9"})
    
     let feed = [];
    
     onMount(async () => {
         
             const {data}  = await devApi.get('/feed')
             feed = data;
             console.log(feed);
             return feed;
        
     })
    
     async function openModal() {
        let userPost = {};
        let result:any  = await showModal({
                page: PostModal,
                props: { userPost: userPost },
            });
            updates = [result, ...updates];
        
    }
     
    
    const setProgressBarWidth = (percent) => {
         let columnStr = '';
        columnStr = percent + "*," + (100 - percent) + "*";
        return columnStr;
     }
    
    </script>
    
    <style>
    
    .figures {
            
            text-align: center;
            font-size:70%;
            color: #E1BC29;
        }
        .progressbar {
            height: 20;
            margin: 10;
            border-radius: 10;
            border-color: black;
            border-width: 2;
        }
        .progressbar-value {
            background: #E1BC29;
            border-radius: 10;
        
        }
        .progressPage {
            background-color: #4D9DE0;
        }
        .list-background {
            background-color: honeydew;
            border: 10px;
            margin: 5px;
            border-radius: 5;
        }
    
    </style>
    
    <page >
        <stackLayout >
            <bottomNavigation>
                <tabStrip>
                    <tabStripItem>
                        <label text="Home" />
                        <image src="font://&#xf015;" class="fas t-36" />
                    </tabStripItem>
                
                    <tabStripItem>
                        <label text="Progress" />
                        <image src="font://&#xf012;" class="fas fa-signal" />
                    </tabStripItem>
                </tabStrip>
    
    
                <tabContentItem class="layout">
                    <stackLayout >
                          <button on:tap="{() => {openModal()}}"text="Post" class="button"></button>
                          
                        <listView margin="10" items="{feed}"> 
                        <Template let:item>
                            <stackLayout >
                                <gridLayout columns="50, 50" rows="*, *">
                                    <image  col="0" row="0" class="-thumb img-circle" src="{item.avatar}" />
                                    <label fontWeight="bold" col="1" row="0" text="{item.user}" />
                                </gridLayout>
                                <stackLayout height="300" >
                                    <label col="0" row="1" class="text-left" text="{item.postBody}" />
                                    <scrollView orientation="horizontal">
                                        <stackLayout orientation="horizontal" >
                                            <image src="{item.picture}"/>
                                            <image src="{item.picture}"/>
                                            <image src="{item.picture}"/>
                                        </stackLayout>
                                    </scrollView>
                                </stackLayout>
                                <button on:tap={() => navigate({ page: Comments, props: {postId: item.postId}})} text="View comments" class="button"/>
                                
                            </stackLayout>
                        </Template>
                        </listView>
                    </stackLayout>
                </tabContentItem>
    
    
                
    
                <tabContentItem class="layout progressPage">
                    <listView items="{users}">
                        <Template class="list-background" margin="10"  let:item>
                            <stackLayout class="list-background"  >
                                <gridLayout columns="50, 50" rows="*, *">
                                    <image  col="0" row="0" class="-thumb img-circle" src="{item.profilePic}" />
                                    <label fontWeight="bold" col="1" row="0" text="{item.user}" />
                                </gridLayout>
                                <stackLayout height="300">
                                    <label class="h2" text="Miles completed this week: {item.milesCompletedThisWeek}"/>
    
    
    
                                    <gridLayout columns="{setProgressBarWidth(item.percentComplete)}" class="progressbar">
                                       
                                       
                                        <stackLayout  col="0" class="progressbar-value">
                                        <label col="0" text="test" />
                                        </stackLayout>
                                      </gridLayout>
    
    
    
                                      <gridLayout columns="*, *" rows="*, *">
                                          <label class="h3" col="0" row="0" text="Total miles completed:"/>
                                          <label class="figures" text="{item.totalMilesCompleted}" col="0" row="1" />
          
          
                                          <label class="h3"  col="1" text="Week streak:" />
                                          <label class="figures" col="1" row="1" text="{item.weekStreak}"/>
    
                                      </gridLayout>
    
    
    
    
                                </stackLayout>
                            </stackLayout>
    
                        </Template>
                    </listView>
    
                </tabContentItem>
            </bottomNavigation>
            </stackLayout>
    </page>