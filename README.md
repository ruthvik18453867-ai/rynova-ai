# rynova-ai
Rynova AI - A general-purpose AI assistant created by Ruthvik Aravind.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Rynova AI</title>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
}

body{
  font-family:Arial,Helvetica,sans-serif;
  background:#0b1020;
  color:#ffffff;
  height:100vh;
  overflow:hidden;
}

.app{
  display:flex;
  height:100vh;
}

/* SIDEBAR */

.sidebar{
  width:260px;
  background:#070b15;
  border-right:1px solid #252d40;
  padding:20px;
  display:flex;
  flex-direction:column;
}

.logo{
  font-size:26px;
  font-weight:bold;
  margin-bottom:25px;
}

.logo span{
  color:#756cff;
}

.new-chat{
  width:100%;
  padding:12px;
  border-radius:10px;
  border:1px solid #303950;
  background:#151c30;
  color:white;
  cursor:pointer;
  font-size:15px;
}

.new-chat:hover{
  background:#202a43;
}

.history-title{
  margin-top:25px;
  margin-bottom:10px;
  color:#78839b;
  font-size:11px;
}

.history{
  color:#b5bdd0;
  font-size:13px;
  overflow:auto;
}

.owner{
  margin-top:auto;
  color:#69748b;
  font-size:11px;
  text-align:center;
}

/* MAIN */

.main{
  flex:1;
  display:flex;
  flex-direction:column;
  min-width:0;
}

.topbar{
  height:64px;
  border-bottom:1px solid #252d40;
  display:flex;
  align-items:center;
  padding:0 24px;
  font-size:18px;
  font-weight:bold;
}

.badge{
  margin-left:8px;
  color:#8792aa;
  border:1px solid #303950;
  border-radius:20px;
  padding:4px 8px;
  font-size:9px;
}

/* CHAT */

.messages{
  flex:1;
  overflow-y:auto;
  width:100%;
  max-width:900px;
  margin:auto;
  padding:30px;
}

.welcome{
  text-align:center;
  margin-top:18vh;
}

.welcome h1{
  font-size:42px;
  margin-bottom:10px;
}

.welcome p{
  color:#929db5;
}

.message{
  display:flex;
  gap:12px;
  margin:22px 0;
  line-height:1.6;
}

.avatar{
  width:36px;
  height:36px;
  min-width:36px;
  border-radius:10px;
  background:#29334f;
  display:flex;
  justify-content:center;
  align-items:center;
  font-weight:bold;
}

.user-avatar{
  background:#6158ed;
}

.message-text{
  padding-top:5px;
  white-space:pre-wrap;
}

/* INPUT */

.composer{
  padding:15px 20px 20px;
}

.input-box{
  max-width:900px;
  margin:auto;
  display:flex;
  padding:7px;
  border:1px solid #303950;
  background:#12192b;
  border-radius:15px;
}

.input-box input{
  flex:1;
  min-width:0;
  border:none;
  outline:none;
  background:transparent;
  color:white;
  font-size:16px;
  padding:12px;
}

.input-box input::placeholder{
  color:#707b93;
}

.send{
  border:none;
  background:#6259ef;
  color:white;
  border-radius:10px;
  padding:0 20px;
  font-weight:bold;
  cursor:pointer;
}

.send:hover{
  background:#756cff;
}

.disclaimer{
  text-align:center;
  color:#606b83;
  font-size:11px;
  margin-top:8px;
}

/* MOBILE */

@media(max-width:700px){

  .sidebar{
    display:none;
  }

  .topbar{
    padding:0 15px;
  }

  .messages{
    padding:20px 15px;
  }

  .welcome h1{
    font-size:32px;
  }

  .composer{
    padding:10px;
  }

  .send{
    padding:0 14px;
  }
}
</style>
</head>


<body>

<div class="app">

<!-- SIDEBAR -->

<aside class="sidebar">

  <div class="logo">
    ✦ <span>Rynova</span> AI
  </div>

  <button class="new-chat" onclick="newChat()">
    ＋ New chat
  </button>

  <div class="history-title">
    RECENT CHATS
  </div>

  <div class="history" id="history"></div>

  <div class="owner">
    Created by Ruthvik Aravind
  </div>

</aside>


<!-- MAIN -->

<main class="main">

  <div class="topbar">
    ✦ Rynova AI

    <span class="badge">
      AI ASSISTANT
    </span>
  </div>


  <!-- MESSAGES -->

  <section class="messages" id="messages">

    <div class="welcome" id="welcome">

      <h1>
        How can I help?
      </h1>

      <p>
        Ask Rynova anything.
      </p>

    </div>

  </section>


  <!-- MESSAGE BOX -->

  <div class="composer">

    <div class="input-box">

      <input
        id="userInput"
        type="text"
        placeholder="Message Rynova AI..."
        autocomplete="off"
      >

      <button
        class="send"
        onclick="sendMessage()"
      >
        Send
      </button>

    </div>

    <div class="disclaimer">
      Rynova AI • Created by Ruthvik Aravind
    </div>

  </div>

</main>

</div>


<script>

/* ELEMENTS */

const input =
document.getElementById("userInput");

const messages =
document.getElementById("messages");

const history =
document.getElementById("history");


/* ADD MESSAGE */

function addMessage(text, sender){

  const welcome =
  document.getElementById("welcome");

  if(welcome){
    welcome.remove();
  }

  const message =
  document.createElement("div");

  message.className =
  "message";

  const avatar =
  document.createElement("div");

  avatar.className =
  "avatar";

  if(sender === "user"){

    avatar.classList.add(
      "user-avatar"
    );

    avatar.textContent = "U";

  }else{

    avatar.textContent = "✦";

  }

  const messageText =
  document.createElement("div");

  messageText.className =
  "message-text";

  messageText.textContent =
  text;

  message.appendChild(avatar);

  message.appendChild(messageText);

  messages.appendChild(message);

  messages.scrollTop =
  messages.scrollHeight;
}


/* DEMO RESPONSE */

function rynovaResponse(question){

  const q =
  question.toLowerCase();

  if(
    q.includes("hello") ||
    q.includes("hi") ||
    q.includes("hey")
  ){

    return "Hello! 👋 I'm Rynova AI. How can I help you today?";

  }

  if(q.includes("who are you")){

    return "I'm Rynova AI, a general-purpose AI assistant created by Ruthvik Aravind.";

  }

  if(q.includes("what can you do")){

    return "I can help with questions, explanations, writing, brainstorming, coding, learning and many other tasks.";

  }

  if(q.includes("business")){

    return "I can help you create business ideas, business plans, budgets, marketing strategies and growth plans.";

  }

  if(q.includes("rynova")){

    return "Rynova AI is a general-purpose AI assistant designed to help users think, create and discover.";

  }

  return "Your message reached Rynova AI. This version is the frontend prototype. Connect a real AI model through a secure backend to generate live AI answers.";

}


/* SEND */

function sendMessage(){

  const question =
  input.value.trim();

  if(question === ""){
    return;
  }

  addMessage(
    question,
    "user"
  );

  input.value = "";

  setTimeout(function(){

    const response =
    rynovaResponse(question);

    addMessage(
      response,
      "ai"
    );

  },500);


  /* HISTORY */

  const item =
  document.createElement("div");

  item.style.padding =
  "8px 2px";

  item.textContent =
  question.length > 30
  ? question.substring(0,30) + "..."
  : question;

  history.prepend(item);
}


/* NEW CHAT */

function newChat(){

  messages.innerHTML = `

    <div class="welcome" id="welcome">

      <h1>
        How can I help?
      </h1>

      <p>
        Ask Rynova anything.
      </p>

    </div>

  `;

  input.focus();
}


/* ENTER TO SEND */

input.addEventListener(
  "keydown",
  function(event){

    if(event.key === "Enter"){
      sendMessage();
    }

  }
);

</script>

</body>
</html>
