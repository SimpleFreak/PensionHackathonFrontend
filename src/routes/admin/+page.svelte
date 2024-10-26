<script>
// @ts-nocheck
import Cookies from 'js-cookie'
  import { onMount } from 'svelte';
  import Users from '../../components/Users.svelte';
let role = ''

Cookies.set('role', 'user')
function checkRole(){

}
onMount(async () =>{
    role = Cookies.get('role')
} )
</script>

{#if role=='admin'}
<div class="container">
    <Users></Users>
</div>
    
{:else}
<div class="container">
    Permission denied
</div>
{/if}
<style>
.container{
    max-width: 1080px;
    margin: 0px auto;
    display: flex;
    flex-direction: column;
    background-color: #fff;
}

</style>