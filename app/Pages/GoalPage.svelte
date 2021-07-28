<script lang="typescript"> 
    import {Template} from 'svelte-native/components'
 let updates: { user: string, post: string }[] = [{user: 'Lee', post: 'Just got back from a 450 mile ride, too easy'}, {user: 'Harry', post: 'I love bikes me'}, {user: 'Chris', post: 'Quick 5 miles'},{user: 'John', post: 'Big ride planned this weekend!!'}]

//  let newUpdate: { user: string, post: string } = {user: 'Lee', post: ''};
 let newPost: { user: string, post: string } = {user: 'Lee', post: ''};
 

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

<page>
<stackLayout>
    <label text="GoalPage" fontSize="50"/>
    <gridLayout columns="3*, *" class="progressbar">
        <stackLayout col="0" class="progressbar-value"></stackLayout>
      </gridLayout>
      <!-- Need to make hint faded -->
      <textField bind:text="{newPost.post}" hint="post an update" ></textField>
      <button on:tap="{addUpdate}"text="Post"></button>
      <!-- need to make height full screen -->
    <listView height="600" items="{updates}"> 
    <Template let:item>
        <label text="{item.user}" />
        <label text="{item.post}" />
    </Template>
    </listView>


</stackLayout>


</page>