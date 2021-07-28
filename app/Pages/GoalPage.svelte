<script lang="typescript"> 
    import {Template} from 'svelte-native/components'
 let updates: { user: string, post: string }[] = [{user: 'Chris', post: 'Quick 5 miles'},{user: 'John', post: 'Big ride planned this weekend!!'}]

 let newUpdate: { user: string, post: string } = {user: 'Lee', post: 'Lets go!'};
 let post: string = "";

 const addUpdate = () => {
    updates = [...updates, newUpdate]
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
      <textField bind:text="{newUpdate.post}" hint="post an update"></textField>
      <!-- test -->
      <button on:tap="{addUpdate}"text="Post"></button>
    <listView height="200" items="{updates}">
    <Template let:item>
        <label text="{item.user}" />
        <label text="{item.post}" />
    </Template>
    </listView>


</stackLayout>


</page>