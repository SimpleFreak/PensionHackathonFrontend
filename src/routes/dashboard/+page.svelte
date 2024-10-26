<script>
// @ts-nocheck

import Radio from "../../components/Radio.svelte";
import Diagrams from "../../components/Diagrams.svelte";
import Table from "../../components/Table.svelte";
import { onMount } from "svelte";
let radioValue='PERSONS';
let error = '';
export let users;
onMount(async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users', {
          method: 'GET',
          mode: 'cors',
          headers: { 'Content-Type': 'application/json' },
        });
        users = response.json()
      } catch (err) {
        error = 'Ошибка подключения';
      }
    });
const casesBot =[
    {

    }
]
const casesWeb = [
  {
    title: "https://mowio.joinsport.io/",
    subtitle: "Mowio. Видео афиши"
  },
  {
    title: "https://reserveproject.ru/",
    subtitle: "Reserve Project. Система бронирования"
  }]


	const options = [{
		value: 'red',
		label: 'PERSONS',
	}, {
		value: 'blue',
		label: 'DIAGRAMS',
	}]
</script>

<div class="container">
    <Radio {options} bind:userSelected={radioValue}></Radio>
    {#if radioValue == "PERSONS"}
      <Table {users}></Table>
    {:else if radioValue == "DIAGRAMS"}
      <Diagrams {casesBot} {casesWeb} {radioValue}></Diagrams>
    {:else}
      <Diagrams {casesBot} {casesWeb} {radioValue}></Diagrams>
    {/if}
</div>


<style>
.container{
    max-width: 1080px;
    margin: 0px auto;
}
</style>