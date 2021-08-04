<script lang="typescript">
    import CommentModal from './CommentModal.svelte';
    import {showModal} from 'svelte-native';
    import {Template} from 'svelte-native/components';
    import { onMount } from 'svelte';
    import axios from 'axios/dist/axios';

// let comments = [{user: 'Lee', profilePic: "~/Images/blankProfilePic.png", commentBody: 'Wow, really impressive!' }]
    export let postId;

    async function openModal() {
        let userComment = {};
        let result: any = await showModal({
                page: CommentModal,
                props: { userComment, postId },
            });
        comments = [result, ...comments];
    }


    const pic = [{ picture: 'https://ftw.usatoday.com/wp-content/uploads/sites/90/2019/09/crying-cyclist.jpg?w=1000&h=576&crop=1'}]


    const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/XGqXEyOP0AanWsqyRqj9"})

    let comments = [];

    onMount(async () => {
        const {data}  = await devApi.get(`/feed/${postId}`)
        comments = data;
        console.log(postId);
        return comments;
    })
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
        .commentsPage {
            background-color: #4D9DE0;
        }
        .commentButton {
            border-radius: 5px;
        }
        .list-background {
            background-color: honeydew;
            border: 10px;
            margin: 5px;
            border-radius: 5;
        }
    
    </style>

<page>


    
    <stackLayout class="commentsPage" >
        <label  class="text-left header" text="Comments" fontSize="20"/>
         <button class="commentButton"  text="Post a comment" on:tap="{() => {openModal()}}" />

  
            <stackLayout>
                <image src="https://ftw.usatoday.com/wp-content/uploads/sites/90/2019/09/crying-cyclist.jpg?w=1000&h=576&crop=1" />
            </stackLayout>
            <listView items="{comments}"> 
                <Template let:item>
                    <stackLayout class="list-background"  >
                        

                            <gridLayout columns="50, 50" rows="*, *">
                                <!-- <image  col="0" row="0" class="-thumb img-circle" src="{item.profilePic}" /> -->
                                <label fontWeight="bold" col="1" row="0" text="{item.username}" />
                            </gridLayout>
                        <label class="text-left" text="{item.commentBody}" />
                            
                            
                        
                    </stackLayout>
                </Template>
             </listView>
    </stackLayout>
</page>

