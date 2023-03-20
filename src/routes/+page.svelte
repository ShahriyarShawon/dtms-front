<script>
import { onMount } from 'svelte';

async function search_classes() {
    let course_number = document.getElementById("drexel_class").value;
    console.log(course_number);
    fetch(`http://localhost:8000/prereqs_for/${course_number}`)
        .then(response => {
            let content = response.json()
        })
}
</script>
<input type="text" name="drexel_class" id="drexel_class" placeholder="Class">
<input type="submit" value="Search" on:click={search_classes}>