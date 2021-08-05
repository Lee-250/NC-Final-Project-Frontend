<script lang="typescript"> 
    import {navigate} from "svelte-native";
    import axios from 'axios/dist/axios';
    import { onMount } from 'svelte';
    import {Template} from 'svelte-native/components';
    import {showModal} from 'svelte-native';
    import PostModal from './PostModal.svelte'; 
    import Comments from './Comments.svelte';

    const loggedInUser = "Lee250";
    
  
    const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/tJgU7tw7OYIlQ88spYlt"})

    let feed = [];
    let users = [];

    onMount(async () => {
        const {data}  = await devApi.get('/feed');
        feed = data;
    })

    onMount(async () => {
        const {data}  = await axios.get('https://us-central1-final-project-backend-16738.cloudfunctions.net/app/users');
        users = data;
    })

    async function openModal() {
        await showModal({
            page: PostModal,
            props: {loggedInUser, users, feed: feed},
        });    
        const {data}  = await devApi.get('/feed');
        feed = data;
    }
     
    const setProgressBarWidth = (percent) => {
         let columnStr = '';
        columnStr = percent + "*," + (100 - percent) + "*";
        return columnStr;
    }
</script>
    
<style>
    .figure {
        
        /* text-align: center; */
        margin-left: 30;
        font-size:70%;
    }
    .figure2 {
        margin-left: 70;
        font-size:70%;
    }
    .week-streak {
        margin-left: 30;
    }
    .total-miles {
        margin-left: 28;
    }
    .progressbar {
        height: 20;
        margin: 10;
        border-radius: 10;
        border-color: black;
        border-width: 2;
        margin-bottom: 50;
    }
    .progressbar-value {
        background: #33ff00;
        border-radius: 10;
    
    }
    .week {
        margin-left: 30;
    }
    .list-background {
        background-color: rgb(255, 255, 255);
        border: 10px;
        border-radius: 35%;
        /* flex: auto; */
        /* margin-bottom: 20;
        margin-top: 10; */
        
    }
    .layout {
        background-image: url("~/Images/Timber.jpg");
        background-position: left;
    }
    .button-comments {
        background-color: rgb(255, 255, 255);
        border-style: solid;
        border-width: 5px;
        border-color: black;
        color: black;
        text-align: center;
        font-size: 16px;
        border-radius: 50%;
        margin-left: 230;
        width: 110;
    }
    .button-post {
        background-color: rgb(255, 255, 255);
        color: black;
        text-align: center;
        font-size: 16px;
        border-radius: 50%;
        width: 140;
    }
    .grid-layout {
        margin-top: 22;
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
                    <gridLayout columns="250, 150" rows="40, 40" class="grid-layout">
                      <button on:tap="{() => {openModal()}}"text="Post" class="button-post" col="1" row="0"></button>
                      <label col="0" row="0" text="Achieve 🏆"
                      fontSize="40"
                      horizontalAlignment="center"
                      color="white"
                      fontWeight="bold" />
                    </gridLayout>
                    <listView items="{feed}"> 
                    <Template let:item>
                        <stackLayout class="list-background">
                            <gridLayout columns="50, auto, *" rows="*, *">
                                <image  col="0" row="0" src="{item.avatar}" class="-thumb img-circle"/>
                                <label fontWeight="bold" col="1" row="0" text="{item.user}:" fontSize="18"/>
                                <label col="2" row="0" text="{item.postBody}" fontSize="18" textWrap="true"/>
                            </gridLayout>
                            {#if item.imageURL}
                            <stackLayout height="300" >
                                <scrollView orientation="horizontal">
                                    <stackLayout orientation="horizontal" >
                                        <image src="{item.imageURL}"/>
                                        <!-- <image src="{item.picture}"/>
                                        <image src="{item.picture}"/> -->
                                    </stackLayout>
                                </scrollView>
                            </stackLayout>

                            {/if}
                                <gridLayout columns="*, 60, 50" rows="20">
                                    <label col="0" text="{item.comments.length} comments" />
                                    <label class ="pull-left" col="1" text="Comment" />
                                    <image  col="2" row="0" on:tap={() => navigate({ page: Comments, props: {postId: item.postId, imageURL: item.imageURL}})}  src="font://&#xf27a;" class="far fa-comment-alt" />

                                </gridLayout>
                            
                            <!-- <button on:tap={() => navigate({ page: Comments, props: {postId: item.postId}})}  text="Comments" class="button-comments"/> -->
                                
                        </stackLayout>
                    </Template>
                    </listView>
                </stackLayout>
            </tabContentItem>
            <tabContentItem class="layout">
                <listView items="{users}">
                    <Template let:item>
                        <stackLayout class="list-background" >
                            <gridLayout columns="50, auto" rows="*, *">
                                <image  col="0" row="0" class="-thumb img-circle" src="{item.avatar}"/>
                                <label fontWeight="bold" col="1" row="0" text="{item.username}" fontSize="22"/>
                            </gridLayout>
                            <stackLayout height="290">
                                <label class="week" text="Miles completed this week: {item.progress}" fontSize="22"/>
                                <gridLayout columns="{setProgressBarWidth((item.progress/50) * 100)}" class="progressbar">                                                                 
                                     <stackLayout  col="0" class="progressbar-value">
                                    <label col="0" text="test" />
                                    </stackLayout>
                                  </gridLayout>
                                  <gridLayout columns="*, *" rows="30, *">
                                      <label class="total-miles" col="0" row="0" text="Total miles:" fontSize="22"/>
                                      <label class="figure" text="{item.totalProgress}" col="0" row="1" fontWeight="bold"/>   
                                      <label class="week-streak"  col="1" text="Week streak:" fontSize="22"/>
                                      <label class="figure2" col="1" row="1" text="{item.weekStreak}" fontWeight="bold"/>
                                  </gridLayout>
                            </stackLayout>
                        </Template>
                    </listView>
                </tabContentItem>
            </bottomNavigation>
            </stackLayout>
    </page>