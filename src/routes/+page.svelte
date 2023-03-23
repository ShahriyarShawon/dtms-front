<svelte:head>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/fabric.js/500/fabric.min.js"></script>
</svelte:head>

<script>
import { onMount } from 'svelte';
import  course  from './course.svelte';

let prereqs = [];
let postreqs = [];

async function searchPrereqsFor() {
    const course_number = document.getElementById("course_name").value;

    await fetch(`http://127.0.0.1:8000/prereqs_for/${course_number}`)
        .then(response => response.json().then(data => {
            prereqs = data;
        }))
}

async function searchPostreqFor() {
    const course_number = document.getElementById("postreq_course_name").value;

    await fetch(`http://127.0.0.1:8000/postreq/${course_number}`)
        .then(response => response.json().then(data => {
            postreqs = data;
        }))
}
</script>


<h1>Hello</h1>
<input type="text" id="course_name" placeholder="Enter Course to find its prereqs">
<input type="submit" value="Search" on:click={searchPrereqsFor}> 

{#each prereqs as obj, i}
<li>{obj}</li>
{/each}

<input type="text" id="postreq_course_name" placeholder="Enter Course to find what classes this is a prereq for">
<input type="submit" value="Search" on:click={searchPostreqFor}> 

{#each postreqs as obj, i}
<li>{obj}</li>
{/each}
