<script>
    // @ts-nocheck
    
      import Button from "../components/Button.svelte";
    
        let login = '';
        let password = '';
        let confirmPassword = '';
        let error = '';
        let success = false;
      
        const handleSubmit = async (event) => {
          event.preventDefault();
    

          try {
            const response = await fetch('http://147.45.110.199/Login', {
              method: 'POST',
              mode: 'cors',
              headers: { 'Content-Type': 'application/json' },
              body: JSON.stringify({ login, password })
            });


      
            if (response.ok) {
              success = true;
              error = '';
              login = '';
              password = '';
              confirmPassword = '';
              window.location.href = '/dashboard';
            } else {
              const data = await response.json();
              error = data.message || 'Произошла ошибка при авторизации';
            }
          } catch (err) {
            error = 'Ошибка подключения';
          }
        };
      </script>
    
      <div class="container">
        {#if success}
          <p>Авторизация успешна!</p>
        {/if}
        
        {#if error}
          <p class="error">{error}</p>
        {/if}
        <h1>Авторизация</h1>
        <form on:submit|preventDefault={handleSubmit}>
          <div>
            <label for="login">Имя пользователя:</label>
            <input id="login" type="text" bind:value={login} required />
          </div>
          
          <div>
            <label for="password">Пароль:</label>
            <input id="password" type="password" bind:value={password} required />
          </div>
          
          
          <Button title='Войти'></Button>
        </form>
        </div>
      
      
      <style>
        .container{
          max-width: 1080px;
          margin: 0px auto;
        }
        body{
        background-color: #FBFBFD;
        color: #163309;
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