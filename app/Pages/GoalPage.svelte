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
        users[3].progress = 40
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
        .goal-progressbar {
            height: 30;
            margin: 10;
            border-radius: 3;
            border-color: grey;
            border-width: 1.5;
            margin-bottom: 20;
        }
        .goal-progressbar-value {
            background: white;
            border-radius: 3;
        
        }

        .progressbar {
            height: 30;
            margin: 10;
            border-radius: 3;
            border-color: black;
            border-width: 2;
            margin-bottom: 20;
        }
        .progressbar-value {
            background: gold;
            border-radius: 3;
        
        }
        
        .week {
            margin-left: 30;
        }
        .list-background {
            background-color: rgb(255, 255, 255);
            border: 10px;
            border-radius: 20%;
            /* flex: auto; */
            /* margin-bottom: 20;
            margin-top: 10; */
            
        }
        .layout {
            background-image: url("~/Images/Timber.jpg");
            background-position: left;
        }
    .commentButton {
        margin-bottom: 8;
    }

  .button-post {
    background-color: rgb(255, 255, 255);
    color: black;
    text-align: center;
    font-size: 18px;
    border-radius: 50%;
    width: 140;
  }

  .grid-layout {
      margin-top: 22;
  }

  .commentNum {
      margin-left: 13;
      margin-bottom: 8;
  }
  .fas.fa-trophy {
    margin: 0;
    padding: 0;
    margin-right: 20;
    height: 28;
    width: 28;
    color: white;
  }
  .far.fa-comment-alt {
      margin-bottom: 6;
      margin-right: 2;
  }
  .-thumb.img-circle {
      margin-left: 22;
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
                    <gridLayout columns="194, 50, 150" rows="50" class="grid-layout">
                      <button on:tap="{() => {openModal()}}"text="Post" class="button-post" col="2" row="0"></button>
                      <image col="1" row="0" src="font://&#xf091;" class="fas fa-trophy fa-5x"/>
                      <label col="0" row="0" text="Achieve"
                      fontSize="40"
                      horizontalAlignment="center"
                      color="white"
                      fontWeight="bold" />
                    </gridLayout>
                    <stackLayout>
                        <label  text="Cycle 30 miles per week"
                      fontSize="20"
                      horizontalAlignment="center"
                      color="white"
                      fontWeight="bold"
                      margin-top="10" />
                      
                    </stackLayout>
                    <gridLayout columns="{setProgressBarWidth(57)}" class="goal-progressbar">                                                                 
                        <stackLayout  col="0" class="goal-progressbar-value">
                       <label verticalAlignment="center" class="text-center" text="Day 16" />
                       </stackLayout>
                       <stackLayout col="1">
                        <label verticalAlignment="center" class="text-center" text="Only 12 days to go!" />
                       </stackLayout>
                     </gridLayout>
                    <listView items="{feed}"> 
                    <Template let:item>
                        <stackLayout class="list-background">
                            <gridLayout columns="65, auto, *" rows="57">
                                <image  col="0" row="0" src="{item.avatar}" class="-thumb img-circle"/>
                                <label fontWeight="bold" col="1" row="0" text="{item.user}" fontSize="14"/>
                                <label col="2" row="0" text="{item.postBody}" fontSize="13" textWrap="true"/>
                            </gridLayout>
                            {#if item.imageURL}
                            <stackLayout height="300" >
                                <scrollView orientation="horizontal">
                                    <stackLayout orientation="horizontal" >
                                        <image src="{item.imageURL}"/>
                                        <stackLayout></stackLayout>
                                        <stackLayout></stackLayout>
                                        <stackLayout></stackLayout>
                                        <stackLayout></stackLayout>
                                        <stackLayout></stackLayout>
                                        <stackLayout></stackLayout>
                                        <!-- added above stacklayouts to cause gap between pictures -->
                                        <image src="{item.secondImageURL}"/>
                                    </stackLayout>
                                </scrollView>
                            </stackLayout>

                            {/if}
                                <gridLayout columns="*, 60, 50" rows="22">
                                    <label col="0" text="{item.comments.length} comments" class="commentNum"/>
                                    <label col="1" text="Comment" class="commentButton"/>
                                    <image col="2" row="0" on:tap={() => navigate({ page: Comments, props: {postId: item.postId, imageURL: item.imageURL}})}  src="font://&#xf27a;" class="far fa-comment-alt" />
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
                            <gridLayout columns="65, auto" rows="*, *">
                                <image  col="0" row="0" class="-thumb img-circle" src="{item.avatar}"/>
                                <label fontWeight="bold" col="1" row="0" text="{item.username}" fontSize="22"/>
                            </gridLayout>
                            <stackLayout height="290">

                                <label class="week" text="Week:  3" fontSize="22"/>
                                <gridLayout columns="{setProgressBarWidth((item.progress/50) * 100)}" class="progressbar">                                                                 

                                     <stackLayout  col="0" class="progressbar-value">
                                    <label class="text-center" col="0" text="{item.progress} miles" />
                                    </stackLayout>
                                    <stackLayout col="1" >
                                        <label class="text-center" text="only {50 - item.progress} to go!" />
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