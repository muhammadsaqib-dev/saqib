require('dotenv').config()
const { connect } = require('mongoose')

const prdSchema = require('../schema/products')
const { addListener } = require('../schema/users')


let all_products = async (req, res) => {
    try {
        const db =await connect(process.env.MONGO_URI)
        const all_product =await prdSchema.find()
        res.status(201).json ({products : all_product})
    } 
    catch (error) {
        res.status(400).send(error.message)
    }
    
}
let all_users = async (req, res) => {
    try {
        const db =await connect(process.env.MONGO_URI)
        const all_users =await prdSchema.find()
        res.status(201).json ({users : all_users})
    } 
    catch (error) {
        res.status(400).send(error.message)
    }
    
}
let productByID = async (req, res) => {
    const { id } = req.params;

    try {
        const db = await connect(process.env.MONGO_URI)
        const user = await prdSchema.findOne({ _id: id })
        res.json({ user })

    }
    catch (error) {
        res.status(400).json({ message: error.message })
    }
}
let userByID = async (req, res) => {
    const { id } = req.params;

    try {
        const db = await connect(process.env.MONGO_URI)
        const user = await prdSchema.findOne({ _id: id })
        res.json({ user })

    }
    catch (error) {
        res.status(400).json({ message: error.message })
    }
}
let userByEmail = async (req,res) => {
    const {email} = req.query;
    try {
       const db = await connect(process.env.MONGO_URI)
       const user = await prdSchema.findOne({ email : email})
       res.json({user})

    } 
    catch (error) {
        res.status(400).json({ message: error.message })
    }
}

let productByCategory = async (req, res) => {
    const { all_products } = req.query;

    try {
        const db = await connect(process.env.MONGO_URI)
        const user = await prdSchema.find()
        res.status(201).json({users : all_products})
    }
    catch (error) {
        res.status(400).json({ message: error.message })
    }
}




{/* // const gender = async (req,res) => {
//     const {all_users} = req.query;
//     try {
//        if () {
        
//        }
//         else {
        
//        } 
//     }
//     catch (error) {
//         res.status(400).json({ message: error.message })

//     } */}




// }
module.exports={ all_products, all_users, productByID, userByID, userByEmail, productByCategory }
