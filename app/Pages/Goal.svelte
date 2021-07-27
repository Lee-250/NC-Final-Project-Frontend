<script lang="typescript">
  const items = ["one", "two", "three"] 
</script>

<style>
  .picker {
    background-color: blanchedalmond;
    color: red;
    border-color: brown;
    border-width: 2;
    height: 100;
    vertical-align: middle;
}
</style>

<page>
  <stackLayout>
    <label text="Create Your Goal" fontSize="50"></label>
    <label text="Select a category"></label>
    <listPicker items="{items}" class="picker"></listPicker>
    <label text="What's your group goal"></label>
    <textField hint="eg. cycle 30 miles per week"></textField>
    <label text="Goal date"></label>
    <datePicker></datePicker>
  </stackLayout>
</page>