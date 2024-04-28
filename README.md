# Email Service Source Code




```javascript
const express = require('express')
const nodemailer = require('nodemailer')
const cors = require('cors')
const app = express()
const port = 4000;

app.use(cors());
app.use(express.json({limit:"25mb"}))
app.use(express.urlencoded({limit:"25mb"}))
app.use((req,res,next)=>{
res.setHeader("Access-Control-Allow-Origin","*");
next();
})

function sendEmail({email,subject,message, phoneNumber, checkbox}){
return new Promise((resolve,reject)=>{
var transporter =nodemailer.createTransport({
service:"gmail",
auth:{
user:"your mail address",
pass:"your password"
}
});
const mail_configs = {
from:email,
to:"your email address",
subject:subject,
text:Mesaj: ${message}\nTelefon Numarası: ${phoneNumber}\nKvkk Metni: ${checkbox}
}
    transporter.sendMail(mail_configs, function (error, info){
        if (error) {
            console.log(error);
            return reject({message:`An error occurred`})
        }

        return resolve({message:"email sent succeess"})
    })

})
}
app.get("/", (req, res) => {
sendEmail(req.query)
.then((response)=>res.send(response.message))
.catch((error)=> res.status(500).send(error.message))
})

app.listen(port,()=>{
console.log(nodemailer is listening at http://localhost:${port});
})




# Client Code Example




```javascript
const apiUrl = process.env.NEXT_PUBLIC_MAIL_API_URL;
  const sendmail = (e) => {
    e.preventDefault()
    axios.get(apiUrl,{
      params:{
        email,
        subject,
        message,
        phoneNumber,
        checkbox
      }
    })
    .then(()=>{
      console.log("success");
    })
    .catch(()=>{
      console.log("faild sent mail");
    })
    setCheckBox(false)
  setEmail("")
  setMessage("")
  setPhoneNumber("")
  setSubject("")
  }
```

