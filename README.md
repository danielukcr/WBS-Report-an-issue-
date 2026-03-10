<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Report an Issue</title>

<style>

body{
font-family: Arial;
background:#0f0f10;
color:white;
display:flex;
justify-content:center;
align-items:center;
height:100vh;
margin:0;
}

.container{
width:600px;
background:#1c1d22;
padding:30px;
border-radius:15px;
box-shadow:0 0 20px rgba(0,0,0,0.5);
}

.header{
display:flex;
align-items:center;
gap:15px;
margin-bottom:20px;
}

.header img{
width:60px;
}

.header h1{
margin:0;
flex:1;
text-align:center;
}

.description{
color:#bdbdbd;
margin-bottom:20px;
text-align:center;
}

label{
display:block;
margin-top:15px;
margin-bottom:5px;
}

select,input,textarea{
width:100%;
padding:10px;
border-radius:8px;
border:none;
background:#2a2c31;
color:white;
}

textarea{
min-height:120px;
}

button{
margin-top:20px;
width:100%;
padding:12px;
border:none;
border-radius:10px;
background:#5865f2;
color:white;
font-weight:bold;
cursor:pointer;
}

.status{
margin-top:15px;
padding:10px;
border-radius:8px;
display:none;
}

.success{
background:#1f6f3a;
display:block;
}

.error{
background:#7a1f1f;
display:block;
}

.hidden{
display:none;
}

</style>
</head>

<body>

<div class="container">

<div class="header">
<img src="https://media.discordapp.net/attachments/1478880251714080961/1480344311491989537/Screenshot_2026-03-07_203727-removebg-preview.png">
<h1>Report an issue</h1>
</div>

<div class="description">
Share a problem you'd like to report or feedback about your experience.
</div>

<form id="reportForm">

<label>Issue type</label>
<select id="issueType" required>
<option value="">Select an option</option>
<option>Report an underage user</option>
<option>Issue with application</option>
<option>Issue with Roblox Game</option>
<option>Issue with Discord accessibility</option>
</select>

<div id="details" class="hidden">

<h3 id="helpTitle"></h3>

<label>Description</label>
<textarea id="description" required></textarea>

<label>Discord username</label>
<input id="username" required>

<label>Discord ID</label>
<input id="discordid" required>

</div>

<button type="submit">Submit report</button>

<div id="status" class="status"></div>

</form>

</div>

<script>

const webhook="https://corsproxy.io/?https://discord.com/api/webhooks/1480715076817125396/GRB2w2qmU8OBUyCt2id79w3l7EKzv21pBT_arz3ZK3f6xwuPlgZHQZS-B4C3R5Ei1vUl"

const issueType=document.getElementById("issueType")
const details=document.getElementById("details")
const helpTitle=document.getElementById("helpTitle")
const form=document.getElementById("reportForm")
const status=document.getElementById("status")

issueType.addEventListener("change",()=>{

if(issueType.value){
details.classList.remove("hidden")
helpTitle.textContent="How can we help you with "+issueType.value+"?"
}

})

form.addEventListener("submit",async(e)=>{

e.preventDefault()

const issue=issueType.value
const desc=document.getElementById("description").value
const user=document.getElementById("username").value
const id=document.getElementById("discordid").value

const payload={
content:"<@&1479931827195219998>",
embeds:[
{
title:"New Issue Report",
color:16711680,
fields:[
{name:"Issue Type",value:issue},
{name:"Description",value:desc},
{name:"Discord Username",value:user},
{name:"Discord ID",value:id}
],
timestamp:new Date()
}
]
}

try{

await fetch(webhook,{
method:"POST",
headers:{"Content-Type":"application/json"},
body:JSON.stringify(payload)
})

status.className="status success"
status.textContent="Report submitted successfully."

form.reset()
details.classList.add("hidden")

}catch{

status.className="status error"
status.textContent="Error submitting report."

}

})

</script>

</body>
</html>
