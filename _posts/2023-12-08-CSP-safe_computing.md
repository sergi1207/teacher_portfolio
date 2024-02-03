---
title: Delete Function
layout: base
description: A login screen that interacts with Python and obtains a JWT  
type: ccc
courses: { csp: {week: 18 }}
---

<!-- 
A simple HTML login form with a Login action when the button is pressed.  

The form triggers the login_user function defined in the JavaScript below when the Login button is pressed.
-->
<form action="javascript:login_user()">
    <p><label>
        User ID:
        <input type="text" name="uid" id="uid" required>
    </label></p>
    <p>
        <button>Delete</button>
    </p>
</form>

<!-- 
Below JavaScript code is designed to handle user authentication in a web application. It's written to work with a backend server that uses JWT (JSON Web Tokens) for authentication.

The script defines a function when the page loads. This function is triggered when the Login button in the HTML form above is pressed. 
 -->
<script type="module">
    // uri variable and options object are obtained from config.js
    import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';
    
    function login_user(){
        // Set Authenticate endpoint
        const url = uri + '/api/users/';
        const authOptions = {
          ...options, // This will copy all properties from options
          cache: 'no-cache',
          method: 'DELETE',
          mode: 'no-cors',
          headers: {
              'Content-Type': 'application/json'
          },
          body:{
            uid: document.getElementById("uid").value
          }
      };
      
      // Fetch JWT
      fetch(url, authOptions)
      .then(response => {
          // handle error response from Web API
          if (!response.ok) {
              const errorMsg = 'Login error: ' + response.status;
              console.log(errorMsg);
              return;
          }
      })}
    window.login_user = login_user;
</script>

