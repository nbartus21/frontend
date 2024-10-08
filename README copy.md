# Restaurant Table Reservation and Food Ordering System

## Table of Contents
1. [Introduction](#introduction)
2. [Features](#features)
3. [Prerequisites](#prerequisites)
4. [Project Structure](#project-structure)
5. [Setup and Installation](#setup-and-installation)
6. [Configuration](#configuration)
7. [Running the Application](#running-the-application)
8. [Detailed Feature Explanation](#detailed-feature-explanation)
9. [API Endpoints](#api-endpoints)
10. [Frontend Routes](#frontend-routes)
11. [Customization](#customization)
12. [Troubleshooting](#troubleshooting)

## Introduction

This project is a comprehensive full-stack web application designed for restaurants, integrating table reservation and food ordering functionalities. Built with a React frontend and a Node.js/Express backend, it utilizes MongoDB for data storage, providing a seamless experience for both customers and restaurant staff.

## Features

1. User Authentication and Authorization
2. Table Reservation System
3. Menu Browsing and Food Ordering
4. Shopping Cart Functionality
5. Admin Panel for Restaurant Management
6. Stripe Integration for Secure Payments
7. Push Notifications for Order Updates

## Prerequisites

Before setting up the project, ensure you have the following installed:
- Node.js (v14 or later)
- npm (comes with Node.js)
- MongoDB (local installation or a cloud-hosted instance)

## Project Structure

The project is organized into two main directories:

- `client/`: React frontend application
- `server/`: Node.js/Express backend application

Key directories and files:
- `src/components/`: React components
- `src/pages/`: Main page components
- `src/context/`: React context for state management
- `server/routes/`: API route definitions
- `server/controllers/`: Business logic for API endpoints
- `server/models/`: MongoDB schema definitions

## Setup and Installation

1. Extract the project files to your desired location.

2. Install dependencies for both frontend and backend:
   ```
   cd client
   npm install
   cd ../server
   npm install
   ```

## Configuration

### Backend Configuration

1. In the `server/` directory, Add the following variables to the `.env` file:
   ```
   PORT=5000
   MONGODB_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret_key
   STRIPE_SECRET_KEY=your_stripe_secret_key
   VAPID_PUBLIC_KEY=your_vapid_public_key
   VAPID_PRIVATE_KEY=your_vapid_private_key
   ```

2. MongoDB Setup:
   - For a local MongoDB instance:
     - Install MongoDB from [official website](https://www.mongodb.com/try/download/community)
     - Start the MongoDB service
     - Use `mongodb://localhost:27017/your_database_name` as your `MONGODB_URI`
   - For a cloud-hosted instance (e.g., MongoDB Atlas):
     - Create an account on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
     - Set up a new cluster
     - Obtain your connection string and use it as your `MONGODB_URI`

3. JWT Secret:
   - Generate a strong, random string for your `JWT_SECRET`
   - You can use an online generator or run this command in your terminal:
     ```
     node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
     ```

4. Stripe Setup:
   - Create an account on [Stripe](https://stripe.com)
   - Obtain your secret key from the Stripe dashboard
   - Use this as your `STRIPE_SECRET_KEY`

5. VAPID Keys for Push Notifications:
   - Generate VAPID keys by running:
     ```
     npx web-push generate-vapid-keys
     ```
   - Add the generated public and private keys to your `.env` file

### Frontend Configuration

1. In the root directory, Add the following variables to the `.env` file:
   ```
   VITE_STRIPE_PUBLIC_KEY=your_stripe_public_key
   VITE_VAPID_PUBLIC_KEY=your_vapid_public_key
   ```

2. Obtain your Stripe public key from the Stripe dashboard and use it for `VITE_STRIPE_PUBLIC_KEY`
3. Use the VAPID public key generated earlier for `VITE_VAPID_PUBLIC_KEY`

## Running the Application

1. Start the backend server:
   ```
   cd server
   npm run dev
   ```

2. In a new terminal, start the frontend application:
   ```
   cd client
   npm run dev
   ```

3. Access the application in your browser at `http://localhost:5173`

## Detailed Feature Explanation

### 1. User Authentication and Authorization
- Implementation: `server/routes/auth.js`, `client/src/context/AuthContext.jsx`
- Description: Allows users to register, login, and maintain sessions. Uses JWT for secure authentication.
- Key Files:
  - `server/controllers/authController.js`: Handles user registration and login
  - `client/src/pages/LoginPage.jsx` and `RegisterPage.jsx`: User-facing auth forms

### 2. Table Reservation System
- Implementation: `server/routes/reservationRoutes.js`, `client/src/pages/ReservationPage.jsx`
- Description: Enables users to book tables for specific dates and times.
- Key Features:
  - Real-time availability checking
  - Reservation management for users and admins

### 3. Menu Browsing and Food Ordering
- Implementation: `server/routes/menuRoutes.js`, `client/src/pages/MenuPage.jsx`
- Description: Displays restaurant menu items and allows users to add items to their cart.
- Key Features:
  - Dynamic menu loading from the database
  - Search and filter functionality

### 4. Shopping Cart Functionality
- Implementation: `client/src/context/CartContext.jsx`, `server/routes/cartRoutes.js`
- Description: Manages user's selected items before checkout.
- Key Features:
  - Add/remove items
  - Adjust quantities
  - Persistent cart for logged-in users

### 5. Admin Panel
- Implementation: `client/src/pages/admin/`, `server/routes/adminRoutes.js`
- Description: Provides an interface for restaurant staff to manage various aspects of the system.
- Key Features:
  - Menu item management
  - Reservation overview and management
  - User account management

### 6. Stripe Integration
- Implementation: `server/routes/checkoutRoutes.js`, `client/src/components/CheckoutForm.jsx`
- Description: Processes secure payments for orders.
- Key Features:
  - Secure handling of payment information
  - Integration with the Stripe API for transaction processing

### 7. Push Notifications
- Implementation: `server/utils/pushNotification.js`, `client/src/utils/pushNotification.js`
- Description: Sends real-time updates to admins about the orders and reservations.
- Key Features:
  - Browser-based push notifications
  - Customizable notification content

## API Endpoints

Detailed documentation of API endpoints can be found in `server/routes/`. Key endpoints include:

- `/api/auth`: User authentication
- `/api/menu`: Menu management
- `/api/reservations`: Reservation handling
- `/api/cart`: Shopping cart operations
- `/api/checkout`: Payment processing

## Frontend Routes

- `/`: Home page
- `/menu`: Restaurant menu and ordering interface
- `/reservations`: Table reservation interface
- `/login` and `/register`: User authentication pages
- `/profile`: User profile and order history
- `/admin/*`: Admin dashboard and management interfaces

## Customization

### Modifying the Menu
- Update the menu items in the MongoDB database
- Use the admin interface at `/admin/menu` to make changes

### Changing Restaurant Information
- Update `client/src/Homepage.jsx` with new details

### Styling
- The project uses Tailwind CSS. Modify `client/src/index.css` or component-specific styles.

## Troubleshooting

- Database Connection Issues:
  - Verify MongoDB is running and the connection string is correct
  - Check for any firewall blocking the database port

- Payment Processing Errors:
  - Ensure Stripe API keys are correct and you're in the right mode (test/live)
  - Verify the Stripe webhook is properly set up

- Push Notification Problems:
  - Confirm VAPID keys are correctly set in both frontend and backend
  - Check browser compatibility and permissions

