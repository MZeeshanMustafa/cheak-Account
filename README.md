-# cheak-Account
user cheak account and find account
<!DOCTYPE html>
<html>
<head>
    <title>GitHub Account Search</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-image: url(images\ \(1\).jpg);
        }
        #search-container {
            margin-top: 20px;
        }
        #results {
            display: none;
            margin-top: 20px;
        }

        h1{
            color: aliceblue;
        }

        img{
        height: 95px;
        width: 95px;

        margin-left: -1050px;
        padding-bottom:0px;
        }
    </style>
</head>
<body>
    
       
    <Fieldset><img src="images.jpg" alt="logo" title="zeeshan"><h1>GitHub Account Search</h1></Fieldset>
    
    <div id="search-container">
        <input type="text" id="search-input" placeholder="Enter GitHub Username">
        <button id="search-button">Search</button>
    </div>
    <div id="results">
        <h2>Results</h2>
        <div id="profile-info">
            <img id="avatar" src="" alt="GitHub Avatar">
            <h3 id="username"></h3>
            <p id="bio"></p>
            <a id="profile-link" href="#" target="_blank">Visit GitHub Profile</a>
        </div>
    </div>

    <script>
        const searchInput = document.getElementById("search-input");
        const searchButton = document.getElementById("search-button");
        const resultsContainer = document.getElementById("results");
        const avatar = document.getElementById("avatar");
        const username = document.getElementById("username");
        const bio = document.getElementById("bio");
        const profileLink = document.getElementById("profile-link");

        searchButton.addEventListener("click", () => {
            const username = searchInput.value.trim();

            if (username) {
                fetch(`https://api.github.com/users/${username}`)
                    .then(response => response.json())
                    .then(data => {
                        if (data.message === "Not Found") {
                            displayError("User not found.");
                        } else {
                            displayProfile(data);
                        }
                    })
                    .catch(error => {
                        displayError("An error occurred. Please try again later.");
                    });
            }
        });

        function displayProfile(data) {
            avatar.src = data.avatar_url;
            username.textContent = data.login;
            bio.textContent = data.bio || "No bio available.";
            profileLink.href = data.html_url;
            resultsContainer.style.display = "block";
        }

        function displayError(message) {
            avatar.src = "";
            username.textContent = "";
            bio.textContent = message;
            profileLink.href = "";
            resultsContainer.style.display = "block";
        }
    </script>
</body>
