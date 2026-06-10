# coding-project-template

# coding-project-template

# 🌿 Final Project: Paradise Nursery Shopping Application  
IBM Full-Stack JavaScript Certificate – Course 5: Developing Front-End Apps with React (Module 4)

---

## 📌 Project Overview

In this final project, you will build a shopping cart web application for a plant shop called Paradise Nursery.

The app allows users to browse houseplants, add them to a cart, adjust quantities, and view total costs dynamically.

---

## 🌱 Core Features

### 🏠 Landing Page
- Background image
- Company name
- Description about the company
- Get Started button linking to product page

### 🌿 Product Listing Page
- At least 6 houseplants
- Grouped into at least 2 categories (e.g. Aromatic, Medicinal)
- Each plant includes:
  - Image
  - Name
  - Description
  - Price
  - Add to Cart button

### 🛒 Shopping Cart Page
- Displays all selected plants
- Each item includes:
  - Thumbnail
  - Name
  - Unit price
  - Quantity controls (+ / -)
  - Delete button
  - Subtotal per plant
- Shows total cart cost
- Includes:
  - Continue Shopping button
  - Checkout button (placeholder)

### 🔄 Header (Global Navigation)
- Cart icon with dynamic item count
- Navigation links to all pages

---

## 🎯 Learning Objectives

- Build React functional components
- Use useState and useEffect hooks
- Implement Redux Toolkit state management
- Render dynamic lists using map
- Handle user events and conditional rendering
- Build full shopping cart logic

---

## 🏗️ Task 1: ProductList Component Layout

const plantsArray = "..."

return "(<div className=\"product-grid\"> {plantsArray.map((plant, index) => ( <div key={index}> <img src={plant.image} /> <h3>{plant.name}</h3> <p>{plant.description}</p> <p>{plant.cost}</p> <button onClick={() => handleAddToCart(plant)}>Add to Cart</button> </div> ))} </div>)"

---

### Add to Cart State

const [addedToCart, setAddedToCart] = useState("{}")

---

### Add to Cart Handler

const handleAddToCart = (plant) => {
  dispatch(addItem(plant))
  setAddedToCart((prev) => ({ ...prev, [plant.name]: true }))
}

---

## 🧠 Task 2: Redux State Management (CartSlice)

### addItem Reducer

addItem: (state, action) => {
  const item = state.items.find(i => i.name === action.payload.name)
  if (item) {
    item.quantity++
  } else {
    state.items.push({ ...action.payload, quantity: 1 })
  }
}

---

### removeItem Reducer

removeItem: (state, action) => {
  state.items = state.items.filter(item => item.name !== action.payload)
}

---

### updateQuantity Reducer

updateQuantity: (state, action) => {
  const { name, quantity } = action.payload
  const item = state.items.find(i => i.name === name)
  if (item) {
    item.quantity = quantity
  }
}

---

### Export Actions

export const { addItem, removeItem, updateQuantity } = cartSlice.actions
export default cartSlice.reducer

---

## 🛒 Task 3: CartItem Component

### calculateTotalAmount

const calculateTotalAmount = () => {
  return cartItems.reduce((total, item) => total + item.quantity * parseFloat(item.cost.substring(1)), 0)
}

---

### handleIncrement

const handleIncrement = (item) => {
  dispatch(updateQuantity({ name: item.name, quantity: item.quantity + 1 }))
}

---

### handleDecrement

const handleDecrement = (item) => {
  if (item.quantity > 1) {
    dispatch(updateQuantity({ name: item.name, quantity: item.quantity - 1 }))
  } else {
    dispatch(removeItem(item.name))
  }
}

---

### handleRemove

const handleRemove = (item) => {
  dispatch(removeItem(item.name))
}

---

### handleCheckout

const handleCheckout = (e) => {
  alert("Functionality to be added for future reference")
}

---

## 🔗 Task 4: Redux Integration

dispatch(addItem(product))

const calculateTotalQuantity = () => {
  return cartItems ? cartItems.reduce((total, item) => total + item.quantity, 0) : 0
}

---

## 🏪 Task 5: Store Setup

import { configureStore } from '@reduxjs/toolkit'
import cartReducer from './CartSlice'

const store = configureStore({ reducer: { cart: cartReducer } })

export default store

---

## 🌍 Task 6: Global Provider

import { Provider } from 'react-redux'
import store from './store.js'

<Provider store={store}> <App /> </Provider>

---

## 🚀 Deployment

npm install gh-pages --save-dev

"predeploy": "npm run build", "deploy": "gh-pages -d dist"

base: "/YOUR_REPOSITORY_NAME"

npm run deploy

---

## 🎉 Summary

You built a complete React + Redux shopping cart application with:
- Product listing
- Cart system
- Dynamic updates
- Redux Toolkit integration
- Deployment setup