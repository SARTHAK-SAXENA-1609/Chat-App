Name: Sarthak Saxena <br>
University: Indian Institute of Technology Roorkee<br>
Department: Civil Engineering<br>
Vercel Link: https://chat-app-sarthak-saxena-1609s-projects.vercel.app/



# Real-time Chat Application Design Document

## Overview
This document outlines the system design for a fully responsive, real-time chat application. The app supports real-time messaging, group chat, dynamic themes, and image uploads, leveraging technologies such as **Next.js**, **Pusher**, **MongoDB**, and **Cloudinary**.


## System Architecture

The architecture is divided into three main parts:
- Frontend: Built with Next.js for server-side rendering (SSR) and client-side rendering (CSR) using the app router.
- Backend: Node.js/Express with Next.js API routes handling requests. Pusher is used for real-time updates, while Next-Auth is used for authentication (GitHub and Google OAuth).
- Database: MongoDB is used as the main database to store user information, chat history, and metadata related to images.




## Features
- Real-time chat updates using Pusher
- Group chat functionality
- Ability to delete chat history
- Image hosting via Cloudinary
- Dynamic theme support (Light/Dark mode)
- Fully responsive for both Desktop and Mobile screens




## Technology Stack
- Next.js: The primary framework for the frontend and backend API routes. It was chosen for its powerful server-side rendering, routing, and performance optimization.
- MongoDB: A NoSQL database that efficiently stores chat messages and user data. It was chosen for its flexibility in handling dynamic, schema-less data like chat messages.
- Tailwind CSS: A utility-first CSS framework that enables quick and responsive UI development with minimal CSS overhead.
- Pusher: Chosen for real-time messaging because of its ease of integration, scalability, and reliability.
- Next-Auth: Used for authentication (Google and GitHub OAuth) to simplify user login and session management.
- Cloudinary: A cloud-based image and video management service that allows for secure and scalable media hosting, making it perfect for storing and retrieving user-uploaded images.
- Zustand: Lightweight state management library used to manage global state like the user’s theme preference (dark/light mode).




## Database Design

The database consists of the following main collections:
- **Users**: Stores user details such as username, email, password, and profile image.
- **Conversations**: Stores information about group or individual chats.
- **Messages**: Stores chat messages with references to conversations and users.

### User Schema
```ts
{
  _id: ObjectId,
  name: String,
  email: String,
  hashedPassword: String,
  profileImage: String,
  createdAt: Date,
}
```

### Message Schema
```ts
{
  _id: ObjectId,
  conversationId: ObjectId,
  senderId: ObjectId,
  text: String,
  createdAt: Date,
}
```


## API Design

The system uses REST APIs built with Next.js for communication between the frontend and backend.

### Endpoints

- `POST /api/auth/login`: Handles user login using **NextAuth**.
- `GET /api/conversations`: Fetches a list of all conversations for the logged-in user.
- `POST /api/conversations`: Creates a new conversation.
- `GET /api/messages/:conversationId`: Fetches all messages for a specific conversation.
- `POST /api/messages`: Sends a new message.


## Security

- **NextAuth**: Provides secure authentication for both OAuth (GitHub, Google) and custom credentials.
- **Bcrypt**: Passwords are hashed using **bcrypt** before being stored in the database.
- **Environment Variables**: API keys and secrets are stored securely in environment variables.



## Scalability Considerations

- **Horizontal Scaling**: The application can be deployed across multiple instances for handling more concurrent users.
- **MongoDB**: Sharding can be used to distribute data across multiple servers.
- **Pusher**: Handles real-time communication, ensuring scalability as the number of chat users grows.



## Deployment

The application is deployed on **Vercel** for its ease of deployment and integration with Next.js.

### Environment Variables:
The following environment variables are required:
- `NEXTAUTH_URL`
- `MONGODB_URI`
- `NEXT_PUBLIC_PUSHER_APP_KEY`, `NEXT_PUBLIC_PUSHER_CLUSTER`, `PUSHER_APP_ID`, `PUSHER_SECRET`
- `NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME`, `NEXT_PUBLIC_CLOUDINARY_PRESET_NAME`
- `GITHUB_ID`, `GITHUB_SECRET`
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`

## Project Setup
1. Clone the project from the repository:
   bash
   git clone https://github.com/your-repo.git
   cd your-repo
   
2.  Create an `.env` file:
3.   Inside the `.env` file, add the following environment variables with values from the previous steps:
   - MongoDB connection string
   - Pusher app details (App ID, Key, Secret, Cluster)
   - Cloudinary credentials (Cloud name, upload preset)
   - GitHub and Google OAuth credentials (Client IDs and secrets)
4.   Install the dependencies:
   yarn install
5.   Push the Prisma schema to your MongoDB:
   yarn prisma db push
6.   Generate the Prisma client:
   prisma generate
7.   Run the app locally:
   yarn dev



## Conclusion

This document outlines the system design of a real-time chat application, highlighting the technology stack, database structure, APIs, and security considerations. With its scalable architecture and use of modern web technologies, the system is designed to handle real-time communication efficiently.

