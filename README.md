<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CELEBRAÇÃO - Login</title>
</head>

<body>

<h2>Login</h2>

<form id="loginForm">
  <input id="username" placeholder="Usuário" required>
  <input id="password" type="password" placeholder="Senha" required>
  <button type="submit">Entrar</button>
</form>

<p id="msg"></p>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, doc, getDoc, setDoc } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "SUA_API_KEY",
  authDomain: "adlogin.firebaseapp.com",
  projectId: "adlogin",
  storageBucket: "adlogin.appspot.com",
  messagingSenderId: "SEU_SENDER_ID",
  appId: "SEU_APP_ID"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// cria usuários padrão se não existir
async function initUsers(){
  const users = {
    admin: "1234",
    teste: "1234"
  };

  for (const u in users){
    const ref = doc(db, "users", u);
    const snap = await getDoc(ref);
    if(!snap.exists()){
      await setDoc(ref, { password: users[u] });
    }
  }
}
initUsers();

loginForm.onsubmit = async (e)=>{
  e.preventDefault();
  const u = username.value.toLowerCase();
  const p = password.value;

  const ref = doc(db, "users", u);
  const snap = await getDoc(ref);

  if(!snap.exists()){
    msg.innerText = "Usuário não existe";
    return;
  }

  if(snap.data().password === p){
    msg.innerText = "Login OK";
  }else{
    msg.innerText = "Senha incorreta";
  }
};
</script>

</body>
</html>
