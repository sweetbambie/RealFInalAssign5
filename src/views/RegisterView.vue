<script setup></script>

<template>
  <div class="hero">
    <div class="overlay">
      <div class="navbar">
        <li class="logo">Feminine Flix</li>
        <a href="index.html" class="button login">Login</a>
      </div>
      <div class="form-container">
        <h2>Create an Account</h2>
        <form>
          <input type="text" placeholder="Name" class="input-field" required>
          <input type="email" placeholder="Email" class="input-field" required>
          <input type="password" placeholder="Password" class="input-field" required>
          <button type="submit" class="register">Register</button>
        </form>
      </div>
    </div>
  </div>
</template>

<style>
.logo {
    font-size: 2rem;
    float: left !important;
    font-family: Georgia, 'Times New Roman', Times, serif;
    font-style: italic;
    font-weight: bold;
    margin-left: 8px;
    color: hotpink;
  }
  
  .overlay {
    background-color: rgba(78, 25, 20,0.7);
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: white;
    padding: 20px;
  }
  
  .navbar {
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: 20px;
  }
  
  .navbar h1 {
    font-size: 2rem;
  }
  
  .navbar .login {
    background-color: hotpink;
    color: white;
    padding: 10px 20px;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s;
  }
  
  .navbar .login:hover {
    background-color: rgb(246, 151, 198);
  }
  
  .form-container {
    text-align: center;
    margin-top: 50px;
  }
  
  .form-container h2 {
    font-size: 2rem;
    margin-bottom: 20px;
  }
  
  .input-field {
    padding: 15px;
    width: 300px;
    border-radius: 5px;
    border: 1px solid #ccc;
    margin-bottom: 15px;
    transition: border-color 0.3s;
  }
  
  .input-field:focus {
    border-color: hotpink;
    outline: none;
  }
  
  .register {
    background-color: hotpink;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
  }
  
  .register:hover {
    background-color: rgb(246, 151, 198);
    transform: scale(1.05);
  }
  
  @media (max-width: 600px) {
    .input-field {
      width: 90%;
    }
  
    .navbar h1 {
      font-size: 1.5rem;
    }
  }
</style>