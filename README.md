<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tayaba's Birthday Wishes</title>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-database.js"></script>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            text-align: center;
            color: white;
            margin: 0;
            padding: 0;
        }
        h1 {
            font-size: 36px;
            margin-top: 20px;
            text-shadow: 2px 2px 5px #333;
        }
        .container {
            width: 90%;
            max-width: 500px;
            margin: auto;
            background: rgba(255, 255, 255, 0.2);
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
        }
        input, button {
            width: 90%;
            padding: 10px;
            margin: 10px 0;
            border: none;
            border-radius: 5px;
            font-size: 18px;
        }
        input {
            background: #fff;
            color: #333;
        }
        button {
            background: #ff5e62;
            color: white;
            cursor: pointer;
            transition: 0.3s;
        }
        button:hover {
            background: #ff1e56;
        }
        .wishes {
            margin-top: 20px;
            text-align: left;
            background: rgba(255, 255, 255, 0.3);
            padding: 15px;
            border-radius: 10px;
            max-height: 300px;
            overflow-y: auto;
        }
        .wish {
            background: rgba(255, 255, 255, 0.7);
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 10px;
            color: #333;
        }
    </style>
</head>
<body>

    <h1>🎉 Happy Birthday Tayaba! 🎂</h1>
    <div class="container">
        <h2>আপনার উইশ লিখুন 🎁</h2>
        <input type="text" id="name" placeholder="আপনার নাম লিখুন">
        <input type="text" id="wish" placeholder="আপনার উইশ লিখুন">
        <button onclick="addWish()">উইশ সাবমিট করুন</button>
    </div>

    <div class="container wishes">
        <h2>🎈 উইশ তালিকা 🎈</h2>
        <div id="wishList"></div>
    </div>

    <script>
        // 🔥 Firebase Config (এখানে আপনার Firebase এর config বসাবেন)
        const firebaseConfig = {
            apiKey: "YOUR_API_KEY",
            authDomain: "YOUR_AUTH_DOMAIN",
            databaseURL: "YOUR_DATABASE_URL",
            projectId: "YOUR_PROJECT_ID",
            storageBucket: "YOUR_STORAGE_BUCKET",
            messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
            appId: "YOUR_APP_ID"
        };

        // 🔥 Firebase Initialize
        firebase.initializeApp(firebaseConfig);
        var database = firebase.database();

        // 🌟 উইশ যোগ করা
        function addWish() {
            var name = document.getElementById("name").value.trim();
            var wish = document.getElementById("wish").value.trim();

            if (name === "" || wish === "") {
                alert("অনুগ্রহ করে আপনার নাম এবং উইশ লিখুন!");
                return;
            }

            var wishRef = database.ref("wishes").push();
            wishRef.set({
                name: name,
                wish: wish
            });

            document.getElementById("name").value = "";
            document.getElementById("wish").value = "";
        }

        // 🎈 উইশ দেখানো (সার্ভার থেকে উইশ আনবে)
        database.ref("wishes").on("child_added", function(snapshot) {
            var data = snapshot.val();
            var wishList = document.getElementById("wishList");
            var newWish = document.createElement("div");
            newWish.classList.add("wish");
            newWish.innerHTML = `<strong>${data.name}:</strong> ${data.wish}`;
            wishList.appendChild(newWish);
        });
    </script>
<script type="module">
  // Import the functions you need from the SDKs you need
  import { initializeApp } from "https://www.gstatic.com/firebasejs/11.3.1/firebase-app.js";
  import { getAnalytics } from "https://www.gstatic.com/firebasejs/11.3.1/firebase-analytics.js";
  // TODO: Add SDKs for Firebase products that you want to use
  // https://firebase.google.com/docs/web/setup#available-libraries

  // Your web app's Firebase configuration
  // For Firebase JS SDK v7.20.0 and later, measurementId is optional
  const firebaseConfig = {
    apiKey: "AIzaSyDng1LiKFIyd1kW-108KbditKvh7mW8GW8",
    authDomain: "birthday-wish-for-tayaba.firebaseapp.com",
    projectId: "birthday-wish-for-tayaba",
    storageBucket: "birthday-wish-for-tayaba.firebasestorage.app",
    messagingSenderId: "678988223021",
    appId: "1:678988223021:web:b83b4e3bdd8bc7042a9ea4",
    measurementId: "G-6YDM7RB186"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const analytics = getAnalytics(app);
</script>
</body>
</html>
