<script>
    // @ts-nocheck
    
    import Button from "../components/Button.svelte";
    import { fade, scale } from 'svelte/transition';
    export let isOpen = false; 
    
    let login = '';
    let password = '';
    let confirmPassword = '';
    let role=''
    let error = '';
    let success = false;
    
    function closePopup(){
      window.location.replace('/admin')
    }
        const handleSubmit = async (event) => {
          event.preventDefault();
      
          
          if (password !== confirmPassword) {
            error = 'Пароли не совпадают!';
            return;
          }
          try {
            const response = await fetch('http://147.45.110.199/Register', {
              method: 'POST',
              mode: 'cors',
              headers: { 'Content-Type': 'application/json' },
              body: JSON.stringify({ login, password, role })
            });
      
            if (response.ok) {
              success = true;
              error = '';
              login = '';
              role = ''
              password = '';
              confirmPassword = '';
            } else {
              const data = await response.json();
              error = data.message || 'Произошла ошибка при регистрации';
            }
          } catch (err) {
            error = 'Ошибка подключения';
          }
        };
</script>

{#if isOpen}
<div class="overlay" transition:fade={{ duration: 500 }}>
  <div class="popup" transition:fade={{ duration: 500 }}>
    <div class="container">
        {#if success}
          <p>Регистрация успешна!</p>
        {/if}
        
        {#if error}
          <p class="error">{error}</p>
        {/if}
        <h1>Регистрация нового пользователя</h1>
        <button class="close_btn" onclick={closePopup}>x</button>
        <form onsubmit={handleSubmit}>
          <div>
            <label for="login">Имя пользователя:</label>
            <input id="login" type="text" bind:value={login} required />
          </div>

          <div>
            <label for="role">Роль:</label>
            <select id="role" bind:value={role} required>
              <option value="" disabled selected>Выберите роль</option>
              <option value="Admin">Администратор</option>
              <option value="User">Пользователь</option>
            </select>
          </div>
          
          <div>
            <label for="password">Пароль:</label>
            <input id="password" type="password" bind:value={password} required />
          </div>
          
          <div>
            <label for="confirmPassword">Подтвердите пароль:</label>
            <input class="input" id="confirmPassword" type="password" bind:value={confirmPassword} required />
          </div>
          
          <Button title='Зарегистрироваться'></Button>
        </form>
        </div>
  </div>
</div>
{/if}

<style>
    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 1000;
    }
  
    .popup {
      background: white;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      padding: 20px;
      border-radius: 8px;
      text-align: center;
      
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .container{
      max-width: 1080px;
      margin: 0px auto;
    }
    form {
      display: flex;
      flex-direction: column;
      max-width: 300px;
      margin: auto;
    }
    div {
      display: flex;
      flex-direction: column;
      margin-bottom: 10px;
    }
    .error {
      color: red;
    }
    label{
      font-size: 16px;
      color: #163309;
    }
    input{
      border: 0px;
      padding: 10px;
      background-color: white;
      -webkit-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
      -moz-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
      box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);    
}
</style>