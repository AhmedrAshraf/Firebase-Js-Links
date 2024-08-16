# Firebase-Js-Links

## Adding Firebase to a JavaScript Project
To integrate Firebase into a JavaScript project without using any frameworks like React, follow these steps:

Include Firebase Modules:
Add the necessary Firebase modules directly from the CDN in your HTML file.


```
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-app.js";
  import { getStorage } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-storage.js";
  import { getFirestore,  doc, deleteDoc, setDoc } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore.js";
  import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword } from "https://www.gstatic.com/firebasejs/9.23.0/firebase-auth.js";

  // Your web app's Firebase configuration
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_STORAGE_BUCKET",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
  };

  // Initialize Firebase
  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);    // Firestore
  const auth = getAuth(app);       // Authentication

  function addUser(){
  // Example: Firestore - Adding a document
    db.collection("users").add({
      name: "John Doe",
      email: "johndoe@example.com"
    })
    .then((docRef) => {
      console.log("Document written with ID: ", docRef.id);
    })
    .catch((error) => {
      console.error("Error adding document: ", error);
    });
  }

  
  function deleteUser(){
    // Delete the user document
      deleteDoc(doc(db, "users", user.uid)).then(() => {
        console.log("User document deleted successfully from Firestore.");
      }).catch((error) => {
        console.error("Error deleting user document: ", error);
      });
  }

  function Signin(){
    signInWithEmailAndPassword(auth, "user@example.com", "user_password")
    .then((userCredential) => {
      // User signed in
      const user = userCredential.user;
    }).catch((error) => {
      console.error("Error deleting user document: ", error);
    });
  }

  
   function signUpUser(email, password, name) {
    createUserWithEmailAndPassword(auth, email, password)
      .then((userCredential) => {
        // Signed up successfully
        const user = userCredential.user;

        // Create user document in Firestore
        const userDocRef = doc(db, "users", user.uid);
        setDoc(userDocRef, {
          uid: user.uid,
          name: name,
          email: email,
        }).then(() => {
          console.log("User document created successfully.");
        }).catch((error) => {
          console.error("Error creating user document: ", error);
        });

        console.log("User signed up successfully:", user);
      })
      .catch((error) => {
        console.error("Error during signup: ", error);
      });
  }

  function checkUser(){
    
  // Check if user is logged in
  onAuthStateChanged(auth, (user) => {
    if (user) {
      // User is signed in
      console.log("User is logged in:", user);
      // You can access user information here, e.g., user.uid, user.email, etc.
    } else {
      // No user is signed in
      console.log("No user is logged in.");
    }
  });
  }
  
</script>
```
