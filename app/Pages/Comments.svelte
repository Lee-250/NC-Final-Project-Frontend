<script lang="typescript">
  import CommentModal from './CommentModal.svelte';
  import {showModal} from 'svelte-native';
  import {Template} from 'svelte-native/components';
  import { onMount } from 'svelte';
  import axios from 'axios/dist/axios';

  export let postId;
  export let imageURL;
  
  async function openModal() {
    let userComment = {};
    let result: any = await showModal({
        page: CommentModal,
        props: { userComment, postId },
      });
    comments = [result, ...comments];
  }

  const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/tJgU7tw7OYIlQ88spYlt"})

  let comments = [];

  onMount(async () => {
    const {data}  = await devApi.get(`/feed/${postId}`)
    comments = data;
    console.log(postId);
    return comments;
  })

  let commentBody = "";
  const handleSubmit = async() => {
    const comment = {
      username: "john",
      commentBody,
      avatar: "https://i.imgur.com/4zxIRRj.jpg"
    }
    comments = [comment, ...comments];
    await devApi.put(`/feed/${postId}`, comment);
  }
</script>

<style>
  .commentsPage {
    background-image: url("~/Images/Timber.jpg");
  }
  .commentButton {
    border-radius: 5px;
  }
  .list-background {
    background-color: white;
    border: 10px;
    margin: 5px;
    border-radius: 5;
  }
  textField {
    background-color: rgb(208, 237, 251);
  }
  .img {
    padding: 15;
  }
  .btn {
    background-color: rgb(255, 255, 255);
    color: black;
    text-align: center;
    font-size: 16px;
    border-radius: 50%;
    width: 102;
  }
  .bottom {
    margin-top: 20;
  }
</style>

<page>
  <stackLayout class="commentsPage" >
    <stackLayout class="img">
      <image src="{imageURL}"/>
    </stackLayout>
    <listView height="325" items="{comments}"> 
      <Template let:item>
        <stackLayout  class="list-background"  >
          <stackLayout >
            <scrollView orientation="vertical">
              <gridLayout columns="55, auto, *" rows="60, *" class="grid-layout">
                <image  col="0" row="0" src="{item.avatar}" class="-thumb img-circle"/>
                <label fontWeight="bold" col="1" row="0" text="{item.username}" />
                <label col="2" row="0" text="{item.commentBody}" textWrap="true"/>
              </gridLayout>
            </scrollView>
          </stackLayout>
        </stackLayout>
      </Template>
    </listView>
    <stackLayout class="bottom">
        <gridLayout columns="300, 102" rows="65">
        <textField col="0" row="0" class="--input-border" margin= "10" hint="add a comment..." textAlignment="center" bind:text="{commentBody}"/>
        <button col="1" row="0" text="Submit" class="btn" on:tap="{handleSubmit}" />
      </gridLayout>
    </stackLayout>
  </stackLayout>
</page>

