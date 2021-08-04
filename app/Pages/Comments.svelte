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

    const devApi = axios.create({baseURL: "https://us-central1-final-project-backend-16738.cloudfunctions.net/app/goals/XGqXEyOP0AanWsqyRqj9"})

    let comments = [];

    onMount(async () => {
        const {data}  = await devApi.get(`/feed/${postId}`)
        comments = data;
        console.log(postId);
        return comments;
    })
</script>

<style></style>

<page>
    <stackLayout backgroundColor="#92CD92" class="m-x-auto" >
        <label  class="text-left header" text="Comments" fontSize="20"/>
        <button text="Post a comment" on:tap="{() => {openModal()}}" />
        <listView height="650" rowHeight="60" margin="10" backgroundColor="#E9FDE3"items="{comments}"> 
        <Template let:item>
            <stackLayout>
                <gridLayout columns="50, 50" rows="*, *">
                    <!-- <image  col="0" row="0" class="-thumb img-circle" src="{item.profilePic}" /> -->
                    <label fontWeight="bold" col="1" row="0" text="{item.username}" />
                </gridLayout>
                <stackLayout>
                    <label col="0" row="1" class="text-left" text="{item.commentBody}" />
                </stackLayout>
            </stackLayout>
        </Template>
        </listView>
    </stackLayout>
</page>

