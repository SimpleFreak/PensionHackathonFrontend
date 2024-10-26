<script>
// @ts-nocheck

import { onMount } from 'svelte';

// @ts-ignore
let data = null;
// @ts-ignore
let file = null;
let isLoading = true;
let isDeleting = false;

onMount(async () => {
    isLoading = true
    try{
        const response = await fetch('http://147.45.110.199/GetAllFiles');
        data = await response.json();
    }catch{
        console.log('err getAllFiles')
    }finally{
        isLoading = false
    }

  });

// @ts-ignore
function handleFileChange(event) {
    event.preventDefault();
  file = event.target.files[0];
}
async function getData(){
    console.log('getData')
}
async function deleteData(id){
    try {
        console.log('delete')
      const response = await fetch(`http://147.45.110.199/DeleteFile${id}`, {
        method: 'DELETE'
      });

      if (!response.ok) {
        alert("Ошибка загрузки файла");
      }
      else{
        console.log('ok')
      }
      
      data = data.filter(item => item.id !== id);
    } catch (error) {
      console.error("Произошла ошибка:", error);
    }
}
async function uploadData(){
    // @ts-ignore
    if (!file) return alert("Пожалуйста, выберите файл");

    const formData = new FormData();
    formData.append("file", file);

    try {
        console.log('start upload file')
      const response = await fetch('http://147.45.110.199/UploadFile', {
        method: 'POST',
        mode: 'cors',
        body: formData
      });
      if (response.ok) {
        alert("Файл успешно загружен!");
      } else {
        alert("Ошибка загрузки файла");
      }
    } catch (error) {
            console.log(error)
      console.error("Ошибка:", error);
      alert("Ошибка при отправке файла");
    }
  }
</script>
{#if isLoading}
    <div class="loading-block">
        Загрузка...
    </div>
{:else}
    <div class="title">
        <h1 class="title">Все загруженные файлы</h1>
        <input type="file" accept=".csv" onchange="{handleFileChange}" />
        <button onclick={uploadData} class="title_btn">Загрузить новый файл</button>
    </div>

    {#each data as file}
    <div class="row">
        <div id='{file.id}'>
            <p class="row__title">{file.fileName}</p>
        </div>
        <div>
            <button onclick={getData} class="row__icons-go">Загрузить</button>
            <button onclick={() => deleteData(file.id)} class="row__icons-del">Удалить</button>
        </div>
    </div> 
    {/each}
{/if}


<style>
.title{
    font-size: 32px;
    font-weight: 400;
    display: flex;
    align-content: center;
    justify-content: space-between;
    margin: 0;
}
.title_btn{
    cursor: pointer;
    color: #fff;
    border: 1px solid #163309;
    border-radius: 10px;
    padding: 10px;
    background-color: #163309;
    transition: 0.3s ease all;
    margin-right: 20px;
}
.title_btn:hover{
    transition: 0.3s ease all;
    opacity: 0.7;
}
.row{
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;

}
.row__title{
    font-size: 15px;
}
.row__icons-go{
    cursor: pointer;
    color: #fff;
    border: 1px solid #8da870;
    border-radius: 10px;
    padding: 10px;
    background-color: #8DA870;
    transition: 0.3s ease all;
    margin-right: 20px;
}
.row__icons-go:hover{
    transition: 0.3s ease all;
    opacity: 0.7;
}
.row__icons-del{
    cursor: pointer;
    color: #fff;
    border: 1px solid #6b1a2b;
    border-radius: 10px;
    padding: 10px;
    background-color: #6b1a2b;
    transition: 0.3s ease all;
}
.row__icons-del:hover{
    transition: 0.3s ease all;
    opacity: 0.7;
}
</style>