<script lang="typescript">
        
    import First from "./Pages/First.svelte";
    
    import {navigate} from "svelte-native";
    
    let message: string = "Blank Svelte Native App";
</script>
   

<style>
    
</style>


<page>
<stackLayout paddingBottom ="80">
   <label text="Achieve" fontSize="70" horizontalAlignment="center" color ="white" />
   <image src="~/Images/trophy.png" />
   <button on:tap="{() =>navigate({page: First})}" text="Start" ></button>
</stackLayout>
</page>
