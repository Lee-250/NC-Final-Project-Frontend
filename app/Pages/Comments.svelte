<script lang="typescript">
    import CommentModal from './CommentModal.svelte';
    import {showModal} from 'svelte-native';
    import {Template} from 'svelte-native/components';


let comments = [{user: 'Lee', profilePic: "~/Images/blankProfilePic.png", commentBody: 'Wow, really impressive!' }]

async function openModal() {
    let userComment = {};
    let result: any = await showModal({
            page: CommentModal,
            props: { userComment: userComment },
        });
        comments = [result, ...comments];
    }

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
                    <image  col="0" row="0" class="-thumb img-circle" src="{item.profilePic}" />
                    <label fontWeight="bold" col="1" row="0" text="{item.user}" />
                </gridLayout>
                <stackLayout>
                    <label col="0" row="1" class="text-left" text="{item.commentBody}" />
                </stackLayout>
            </stackLayout>
        </Template>
        </listView>
    </stackLayout>

</page>

