---
title: JWT Signup (python/flask)
layout: base
description: A login screen that interacts with Python and obtains a JWT  
type: ccc
courses: { csp: {week: 18 }}
---

<!-- 
A simple HTML login form with a Login action when the button is pressed.  

The form triggers the login_user function defined in the JavaScript below when the Login button is pressed.
-->
<body>
<form id="signupForm" action="#">
    <p><label>
        User ID:
        <input type="text" name="uid" id="uid" required>
    </label></p>
    <p><label>
        Password:
        <input type="password" name="password" id="password" required>
    </label></p>
    <p><label>
        Dob:
        <input type="date" name="dob" id="dob" required>
    </label></p>
    <p><label>
        Name:
        <input type="text" name="name" id="name" required>
    </label></p>
    <p><label>
        Hobby:
        <input type="text" name="name" id="hobby" required>
    <p>
        <button type="submit">Signup</button>
    </p>
</form>


<!-- 
Below JavaScript code is designed to handle user authentication in a web application. It's written to work with a backend server that uses JWT (JSON Web Tokens) for authentication.

The script defines a function when the page loads. This function is triggered when the Login button in the HTML form above is pressed. 
 -->
<script type="module">
    import { uri, options } from '{{site.baseurl}}/assets/js/api/config.js';

    document.addEventListener('DOMContentLoaded', () => {
        document.getElementById('signupForm').addEventListener('submit', signup_user);
    });

    function signup_user(event) {
        event.preventDefault();

        const url = uri + '/api/users/';

        const body = {
            uid: document.getElementById("uid").value,
            password: document.getElementById("password").value,
            dob: document.getElementById("dob").value,
            name: document.getElementById("name").value,
            hobby: document.getElementById("hobby").value,
        };

        const authOptions = {
            ...options,
            method: 'POST',
            cache: 'no-cache',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(body)
        };

        fetch(url, authOptions)
            .then(response => {
                if (!response.ok) {
                    throw new Error('Signup error: ' + response.status);
                }
                window.location.href = "{{site.baseurl}}/data/database";
            })
            .catch(err => {
                console.error(err.message);
            });
    }
</script>
</body>



