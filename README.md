BACKEND NOTES 

MAIN KNOWLEDGE

api
    data transfer that transfer data in json formate

node.js
       next.js
server
       webbsite
database

json 
     array oof object

diffrence between mangodb and sql ?

. mangodb stores data in json format.
. sql stores data in rows and coloums.

. mangodb does not provide transiction facuilty and are easy to hacked
. sql provide transition facuilty and cannot be eaisly hacked cuz it stores data in rows and colums 


what is backend use in mern stack ?
Nodejs(runtime enviorment that compile our code with backend) , Express.js(to get import or export of data) , MangoDB(database {that stores data}


                                             MAKE PROJECT
lets create project
write command on terminal npm init
then enter all suggestion (yes)
u get packge.json file
then we need to make our server live hence we write in packge.json file 
"script" : {
"start" : node-index.mjs
"dev": nodemon.mjs
}


to get nodemon dependecies {
write on google nodemon  get command on nodemon(npm i nodemon) and paste in terminal u got packge-lock.json and nodemodules. 
then make index.mjs to add express dependencies write on google npm express get command ( npm i express) and u need the first thing in backend import express to run the entire web.

what is mjs?
mjs is a syntax as we used index.js in frontend while in backend we write m with js to make global website while we live our web.


                                     Folder Structure

theres main 3 folders wwhich are made for backend 
routes(where all api routes are placed)
config(to configure or connectin )
models(where mongoDb schema are kept)


                                    TO ADD MONGOD

search mongoose on google run the command (npm install mongoose) then search in mongoose web models we get schema 

what is schema?
its  is use for validation of data come from user 

                                       Create Schema

 lets create Schema

 
                                      Models folder work                            

to make schema 
import mongoos from mongoos
import {schema} from mongoos


there is a way to make variable and store new schema
and then make so on schemas for validation also then export name should be capital .

How to expport schema?

make variable at the end and store mongooes.model(" its a database container of spacific thing where data stored", and place the variable name made above)
then export default  add the variable name where mongoos.model is stored. 

 
                                Config folder work            

write  on terminal  npm i dotenv( for env files)
make environment.mjs file to keep process.env for port and mongo

import dotenv from 'dotenv'

dotenv.config()

export const PORT=process.env.PORT
export const MONGO_URL=process.env.MONGO_URL


now make db.mjs file in  config 

login into mongodb and get  mongo url which are kept in .env file
then use mongooes connection function as 

import mongoose from "mongoose";
import  {MONGO_URL} from './environment.mjs';

mongoose.connect(MONGO_URL)

export default mongoose

mongoos.connect (place  mongose url from env)
and then export the mongoose.


                          Routes folder work

make parent file as index.mjs where all routes are kept to export into main index file of backend folder
import express from express 
make variable to store express.Router()

now to render the api file of product always write router.use("/api file route",api file name)
then make a file the name mention in path "api file name " into  this folder to create api .
to export the main index file write,
export default variable name.

How to render this index router file in main backend index.mjs file?

import express from express
make variable as
let router = express.Router()

to render routes 
router.use("/",router)
where / indicates the main path or the main file of router folder (index.mjs)


                         Make API

to make api following are the types.
get 
get by id
post 
put(that update the existing item)
delete.

import express from express
import {product schema} from "./"

similarly make variable 
 router =  express.Router()


to export write
export default variable name .
                  
                      Make Get API
syntex,

router.get("/ ", async (res,req)=>{
let allproducts = await  field of schema.find()
res.send({ message : " " , Data : allproducts })
})

router .get us a method to get data  where " / " provide main path of api eg:" https api.com/product " then apply arrow function with async that includes parameter (res,req) 
make a variable that holds schema and put .find() on it that find the products and validate according to the schema
apply res.send() in that send  message ,  also a variable name that holds field , data : holds variable name  .

                      Make Get by Id API
syntex,

router.get("/:id",async (req,res)=>{
try{
let singleProduct = await schema name.findById(req.params.id)
res.send({message:"single product fetched successfully",Data:singleProduct})
}
catch(e){
    res.status(500).send({message:e.message})

}
})


where syntx is same like get api , and we make path for get by id  
similarly make variable by applyiing await and schema for validation and apply method findById(which get the id of each product  where req.prams.id  shows the specific product id )
and  then similarly send message after it catch block being appear that show error.

                      Make Post API

syntex ,

 router.post('/post', async (req, res) => {
     try {
         const postProduct = new schema name(req.body)
         await postProduct.save()
         console.log(req.body)
         res.send({ message: 'product posted successfully' })
     } catch (e) {
       res.send({ message: e.message })
     }
 })

all syntex is same but there's diffrence is after schema validation (req.body)shows that data are posted in the body of data similarly like postman.


                         Make Update API

syntex,

router.put('/:id', async (req, res) => {
    try {
        const updatedProduct = await schema name.findOneAndUpdate(
            req.params.id,
            req.body,
           { new: true } // To return the updated document
        );
        res.send({ message: 'Product updated successfully', updatedProduct });
    } catch (e) {
        res.send({ message: 'Error updating ad', error: e.message });
    }
});

where router.put are the method used for updating product where .findOneAndUpdate(
The document id (req.params.id) → find which document to update
and req.body holds the product data  like ( title , price , etc...) and then it set the updatedproduct data into new object 
where new:true return the new object made in the mongodb so that the old object does not appear in api .


                     Make Delete API

syntex,

router.delete('/:id', async (req, res) => {
  try {
    const deletedProduct = await schem name.findByIdAndDelete(req.params.id);

    if (!deletedProduct) {
      return res.status(404).send({ message: ' Product not found ' });
    }

    res.send({ message: ' Product deleted successfully', deletedProduct });
  } catch (e) {
    res.status(500).send({ message: 'Error deleting ad', error: e.message });
  }
});

similarly other api delet api is similar to update where .findByIdAndDelete(req.params.id  is for geting specific product with id and delete it)
and even u can apply earliy case where if deleteProduct not exist it shows error.




what is id means?
there always 3 main id {
product_id
user_id
token( this is generated when user login )

 
                       Make Post API With Image link

for make post api with accessible images we use multer and cloudinary 

                                                  


                      OVERALL NOTES FOR MULTER AND CLOUDINARY
.
Multer kya hai?
Multer ek middleware hai jo Node.js/Express mein file uploads handle karta hai.

Jab user apni taraf se koi image ya file upload karta hai (jaise product ki photo), wo directly request ke sath aati hai, lekin wo data multipart/form-data format mein hota hai.

Normal req.body sirf text handle karta hai, images/files nahi — isliye multer lagate hain.

Multer wo file temporarily local storage (folder) mein save kar deta hai ya memory buffer mein rakhta hai, taake baad mein aap usko kahin upload kar sako (e.g., Cloudinary pe).

📌 Example ka flow:

User → Product form → Image choose ki.

Image HTTP request ke sath backend me aayi.

Multer us image ko read karke temp folder ya memory me rakhta hai.

Ab aap backend me us file ka path leke Cloudinary pe bhej dete ho.

Cloudinary kya hai?
Cloudinary ek cloud storage + image management service hai.

Ispe aap apni images upload kar sakte ho, aur ye automatically unki URL bana deta hai jo aap apni database me save kar sakte ho.

Aapko server pe images permanently store nahi karni padti — Cloudinary unka secure hosting karta hai.

Extra features:

Images ka size compress karna.

Format convert karna (JPG → PNG).

URLs me transformations apply karna (resize, crop, watermark).

📌 Example ka flow:

Multer se image temporary storage me ayi.

Backend se us image ko Cloudinary ke upload API me bheja.

Cloudinary image ko save karke ek public URL return karega.

Aap wo URL apne products collection me store kar loge.

Multer + Cloudinary milke kaise kaam karte hain
Multer ka kaam: File ko request se nikal ke backend me laana.

Cloudinary ka kaam: Backend se file leke online store karna aur URL dena.

Aapke product API me:

Pehle multer middleware lagega.

Fir Cloudinary pe upload ka code chalega.

Fir product ka data + Cloudinary ka URL DB me save hoga


                       HOW TO INTEGRATE MULTER AND CLOUDINARY


write on terminal npm i multer(for multer)
write  on terminal  npm i cloudinary(for clodinary purpose)
 
What is middlewares ?

Middleware ek beech ka function hai jo request aur response ke darmiyan chal kar extra kaam karta hai;
 multer middleware request se file nikal kar req.file me daal deta hai
 aur agar uska storage Cloudinary set karo to wahi file direct Cloudinary pe upload ho jati hai aur uska URL req.file.path me milta hai,
 is tarah route code ko sirf uploaded file ka URL use karna padta hai.




                                                    
                                                Config Folder work

                                                
make cloudinary.mjs file 
import dotenv from "dotenv";

import {v2 as cloudinary} from "cloudinary";


dotenv.config()

cloudinary.config({
  cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
  api_key: process.env.CLOUDINARY_API_KEY,
  api_secret: process.env.CLOUDINARY_API_SECRET
});

export default cloudinary;

where these process.env names are come from .env file that  holds thier keys



                                                          Middleware Folder
make middleware folder
make file in middleware folder with name uploadimg.mjs

import multer from multer
import cloudinary storage from multer-storage-cloud
import cloudinary from 'config '


make variable and store new CloudinaryStorage({
cloudinry : cloudinary,
params:{
folder:'products' 
allowed_format:["jpg",
})


import multer from "multer";
import cloudinary from "../config/cloudinary.mjs"
import pkg from "multer-storage-cloudinary";

const { CloudinaryStorage } = pkg; 


const storage = new CloudinaryStorage({
    cloudinary: cloudinary,
    params: {
        folder: "products",//write folder name that create folder in cloudinary
        allowedFormats: ["jpg", "png", "jpeg"], //it sets the formate of img
        transformation: [{ width: 500, height: 500, crop: "limit" }]
    }
})

const upload = multer({ storage}); //lastly this sets storage in multer that perform as middleware

export default upload;


                         Route Folder Work


               
now in product.mjs file lets integrate cloudinary .

import upload from "../middlewares/uploadimg.mjs";
then add upload.single('image') after the path of post api
then apply this code in try block.

const imageUrl = req.file?.path; // Get the image URL from the uploaded file
        const productData = {
            ...req.body,
            image: imageUrl // Add the image URL to the product data
        };


                              FINAL POST API 


and here is the final post api

router.post('/post',upload.single('image'),async(req,res)=>{
    try{
        const imageUrl = req.file?.path; // Get the image URL from the uploaded file
        const productData = {
            ...req.body,
            image: imageUrl // Add the image URL to the product data
        };

        const postProduct=new Products(productData);
        await 
        postProduct.save() 
        res.send({ message: 'data posted successfully' })
        console.log("data:", req.body);
        
    }
    catch(e){
        res.status(500).send({message:e.message})
    }
})




HOW TO APPLY STRIPE (PAYMENT METHOD)


first make account from stripe and get api key and paste thee api key into env file

write in .env file 
Sectert_key:stripe api key
client_Url; localhost or the api url 


make utils folder  
what does utils folder do ?
its is used to store those data which seccure our data or security purpose

                                           
                                  Utils Folder Work

write commad on terminal npm i stripe
mke stipe file 

import Stripe from 'stripe';
import dotenv from dotenv


then config env as
 dotenv.config()

make variable  and store Stripe and its process.env secret_key from .env file and its api version as 

const stripe = new Stripe(process.env.Stripe_Secret_Key,{
apiVersion : '2024-08-01',
});

export default stripe ;



                                        Route Folder work

then make payment.mjs in route folder for payment api 

import express
import stripe from '../utilss/stripe';


make variable
const router = express.Router();

router.post('/create-checkout-session',async (req,res)=>{
try{
 const {allproduct} = req.body

if(!allproduct?.name  || !allproduct?.price){
return res.status(400).send({message: "invalid product data  "});
}

 const session = await stripe.checkout.sessions.create({
   payment_method_types : ["card"],
    line_items: [
      {
        price_data: {
          currency: 'usd',
          product_data: {
            name: allproduct.name,
            description:allproduct.description,
          },

          unit_amount:allproduct.price*100,
        },
        quantity: 1,
      },
    ],
    mode: 'payment',
    success_url: 'process.envClient_Url /success',
    cancel_url: 'process.envClient_Url /cancel',
  });


 res.send({ url:session.url});

}catch(error){
res.status(500).send({
message:"Stripe checkout session failed",
error: error.message,})
}
});


export default router;

                   

                     Route Folder index.mjs work

import payment file 
and make 
router.use(router.use('/payment', payment);


what is cors?
 Cors ek security feature hai jo browser ko control karta hai ke kis domain se request allow hai;
 Express me cors() middleware use karte hain taa ke hamara API dusre frontend domains (jaise React/Next.js app) se safely access ho sake,
 warna browser cross-origin requests block kar deta hai.

                     
                    How to access cors

CORS use karne ke liye pehle command chalao
 npm install cors,
 phir apni index file me 
import cors from "cors"; 
 app.use(cors()) add karo taa ke API dusre domains se access ho sake.

then agr live krni ho api to localhost hata  ky app.get likho taky is api ko main path mily or vercel my live hony my asani ho

app.get("/", (req, res) => {
  res.send("🚀 API is running on Vercel");
});


                 How to Apply JWT (jsonwebtoken)


what is jwt ?
JWT ek secure token hota hai jo mostly login ke baad authentication aur authorization ke liye use hota hai. 
Jab user login karta hai to backend ek JWT generate karke frontend ko deta hai, jo har request ke header me bheja jata hai.
 Backend is token ko verify karke confirm karta hai ke request ek valid user ki hai aur uske paas kya permissions hain. 
Ye method stateless, secure aur scalable hota hai, is liye modern web apps me bohot use hota hai.

                Lets add jwt into project

                
write on google npm jwt get command.
write( npm i jsonwebtoken ) on terminal

make variable in .env file and store ur own maked jwtsecret.
JWT_SECRET= can place any key word

    
                Config Folder Work

in enviornmental.mjs file make process.envof jwt secret
export const JWT_SECRET=process.env.JWT_SECRET

make jwt.mjs file in config folder to store enovoirnmental.mjs process.env variable.
import { JWT_SECRET } from "./environment.mjs";


const jwtSecret=JWT_SECRET

export default jwtSecret


             Model Folder Work


             
lets make schema for users
cerate a file user.mjs


import mongoose from "mongoose";
import bcrypt from 'bcryptjs';
import jwt from 'jsonwebtoken'
import jwtSecret from "../config/jwt.mjs";


const { Schema } = mongoose;

const userSchema = new Schema({
email: {
    type:String,
    required:true,
    unique:true
},
password: {
    type:String,
    required:true,
    minLength: 6
},
fullname: {
    type:String,
    required:true
},
tokens: {
    default: [],
    type: []
}
});
userSchema.pre('save',function(next){
    const user=this
    //encryption
    if (user.isModified('password')) {
        const salt = bcrypt.genSaltSync(10);
        const hash = bcrypt.hashSync(user.password, salt);
    
        user.password = hash
    }
    next()
})

userSchema.methods.comparePassword = function (password) {
    const user = this

    //user.password === db password (encrypted) asjdhu2i346193
    //password === frontend password (normal) 123456
    console.log('db password', user.password)
    console.log('frontend password', password)
    
    return bcrypt.compareSync(password, user.password)
}

userSchema.methods.generateToken = function() {
    const { _id } = this
    const token = jwt.sign({ _id }, jwtSecret);

    return token
}

const Users = mongoose.model('user', userSchema);

export default Users

 

                  Middleware Folder Work


for which we used jwt is to insure authentication and autherization of user 
due to that we make file in middleware folder verifyToken.mjs for checken balance between authorize user who access permission 
and other user who did'nt a authorized user of website.

import jwt from 'jsonwebtoken';
import Users from '../models/Users.mjs';
import jwtSecret from '../config/jwt.mjs';

async function verifyToken(req, res, next) {
    const token = req.headers.authorization?.split(' ')[1]

    if (!token) {
        res.status(401).send({ message: "No access!" })
        return
    }

    try {
        const decoded = jwt.verify(token, jwtSecret)

        const tokenExists = await Users.findOne({ tokens: token })

        if (!tokenExists) {
            res.status(401).send({ message: "Invalid token!" })
            return
        }

        req.userId = decoded._id
        req.tokenToRemove = token
        next()
    } catch (e) {
        res.status(401).send({ message: "Invalid token!" })
    }
}

export default verifyToken;



                Router Foldeer Work
make file user.mjs

import express from 'express'
import Users from '../models/user.mjs'
import verifyToken from '../middlewares/verifyToken.mjs'

const router=express.Router()

//to get all users
router.get('/',async(req,res)=>{
    const users=await Users.find()
    res.send({message:'Data Fetched Successfully',Data:users})
})

router.post('/register',async(req,res)=>{
    try{
    const user=new Users(req.body)
    await user.save()
    res.send({ message: "User registered successfully!" })
    }
    catch(e){
        res.send({message:e.message})
    }
})

router.post('/login',async(req,res)=>{
    //Step 1: Check if email exists
    try{
        const {email,password}=req.body

        const user=await Users.findOne({email})
    if(!user){
        res.send({message:'User Not Found'})
        return
    }
    //Step 2: Compare the passwords
    const isCorrect=user.comparePassword(password)
    if(!isCorrect){
        res.status(404).send({message:'Invalid Password'})
        return
    }
    //Step 3: Generate Token
    const token = user.generateToken()
    user.tokens.push(token)
    await user.save()

    res.send({ message: 'User logged in successfully!',token })
}
    catch(e){
        res.status(404).send({message:e.messsage})
    }
})

router.put('/logout',verifyToken,async(req,res)=>{
    await Users.findByIdAndUpdate(req.userId, { $pull: { tokens: req.tokenToRemove } })
    res.send({message:'Logged Out Successfully'})
})

export default router


               Router Foldeer index.mjs work
import user file and write in route.use()

import user from './user.mjs'
router.use('/user',user);


 
 


when ever user come always theres 3 main thing that requires for authentiction

email
password 
and then it generate token 


                   How to live API on Vercel

to live Api make vercel.json in root folder.
then add these configurations into the file.

{
  "version": 2,
  "builds": [
    { "src": "index.mjs", "use": "@vercel/node" }
  ],
  "routes": [
    { "src": "/(.*)", "dest": "index.mjs" }
  ]
}

                  Package.json File Work

Make sure tumhare package.json me type: "module" ho agr na ho to khud add krlo
aur dependencies check kro(express, cors, mongoose, etc.) listed hain.









                            MVC{ model view contrller}

sbsy phely yeh 2 chizn edition hongi 
controller
or aik file  bny gi service ki jis m index.mjs main file 
