## 🌐 NEXUS: Real-Time Social Media Platform

## 📌 Overview

NEXUS is a full-stack MERN social media platform where people can share photos and videos, post short video **Loops**, upload 24-hour **Stories**, follow other users, and chat in real time. Likes, comments, follow alerts, new messages, and online status all update instantly through Socket.IO, while media is stored on Cloudinary and accounts are protected with JWT cookies and OTP-based password reset.

## 🚀 Why It Matters

💬 **Real-Time Interaction Keeps Users Engaged**
→ Instant likes, comments, notifications, and chat make a platform feel alive and encourage people to come back.

🎬 **Short Video Is How People Share Today**
→ Loops (short videos) and 24-hour Stories match the content formats users already love.

🔐 **Secure by Design**
→ Password hashing with bcrypt, JWT cookie sessions, and email OTP verification protect user accounts.

## 🏗 Project Structure

```text
📂 NEXUS
├── 📂 backend  (Node.js, Express, MongoDB & Socket.IO)
│   ├── index.js  (Express server entry point & route setup)
│   ├── socket.js  (Socket.IO server, online users & real-time events)
│   ├── package.json  (Backend dependencies)
│   ├── .gitignore
│   ├── 📂 config
│   │   ├── db.js  (MongoDB connection)
│   │   ├── cloudinary.js  (Cloudinary media upload)
│   │   ├── Mail.js  (Nodemailer OTP emails)
│   │   ├── token.js  (JWT token generation)
│   ├── 📂 controllers
│   │   ├── auth.controllers.js  (Signup, signin, signout, OTP & password reset)
│   │   ├── user.controllers.js  (Profile, follow, search, suggestions & notifications)
│   │   ├── post.controllers.js  (Upload, like, comment & save posts)
│   │   ├── loop.controllers.js  (Upload, like & comment on Loops)
│   │   ├── story.controllers.js  (Upload & view Stories)
│   │   ├── message.controllers.js  (Send messages & chat history)
│   ├── 📂 middlewares
│   │   ├── isAuth.js  (JWT cookie authentication middleware)
│   │   ├── multer.js  (File upload handling)
│   ├── 📂 models
│   │   ├── user.model.js  (User schema: profile, followers, saved, OTP fields)
│   │   ├── post.model.js  (Post schema: media, likes, comments)
│   │   ├── loop.model.js  (Loop schema: video, likes, comments)
│   │   ├── story.model.js  (Story schema with 24-hour auto-expiry)
│   │   ├── message.model.js  (Message schema: text & image)
│   │   ├── conversation.model.js  (Conversation schema)
│   │   ├── notification.model.js  (Like, comment & follow notifications)
│   ├── 📂 routes
│   │   ├── auth.routes.js  (Auth endpoints)
│   │   ├── user.routes.js  (User endpoints)
│   │   ├── post.routes.js  (Post endpoints)
│   │   ├── loop.routes.js  (Loop endpoints)
│   │   ├── story.routes.js  (Story endpoints)
│   │   ├── message.routes.js  (Message endpoints)
│   ├── 📂 public
│   │   ├── .gitkeep  (Temporary upload folder placeholder)
│
├── 📂 frontend  (React.js + Redux + TailwindCSS + Vite)
│   ├── index.html  (Base HTML file)
│   ├── package.json  (Frontend dependencies)
│   ├── vite.config.js  (Vite & Tailwind configuration)
│   ├── eslint.config.js  (ESLint configuration)
│   ├── README.md  (Default Vite readme)
│   ├── .gitignore
│   ├── 📂 public
│   │   ├── favicon.png  (Favicon)
│   │   ├── vite.svg
│   ├── 📂 src
│   │   ├── App.jsx  (Main component, routing & Socket.IO client setup)
│   │   ├── main.jsx  (React entry point)
│   │   ├── App.css  (Component styling)
│   │   ├── index.css  (Global TailwindCSS styling)
│   │   ├── 📂 assets  (logo, default profile picture & images)
│   │   ├── 📂 components
│   │   │   ├── Nav.jsx  (Bottom navigation bar)
│   │   │   ├── LeftHome.jsx  (Left sidebar: notifications & suggestions)
│   │   │   ├── RightHome.jsx  (Right sidebar)
│   │   │   ├── Feed.jsx  (Home feed with Stories & Posts)
│   │   │   ├── Post.jsx  (Post card with like, comment & save)
│   │   │   ├── LoopCard.jsx  (Loop video card)
│   │   │   ├── VideoPlayer.jsx  (Custom video player)
│   │   │   ├── StoryDp.jsx  (Story profile bubble)
│   │   │   ├── StoryCard.jsx  (Story viewer)
│   │   │   ├── FollowButton.jsx  (Follow/unfollow button)
│   │   │   ├── OtherUser.jsx  (Suggested user card)
│   │   │   ├── OnlineUser.jsx  (Online user in chat list)
│   │   │   ├── NotificationCard.jsx  (Single notification)
│   │   │   ├── SenderMessage.jsx  (Sent chat message bubble)
│   │   │   ├── ReceiverMessage.jsx  (Received chat message bubble)
│   │   ├── 📂 pages
│   │   │   ├── SignUp.jsx  (Registration page)
│   │   │   ├── SignIn.jsx  (Login page)
│   │   │   ├── ForgotPassword.jsx  (OTP-based password reset)
│   │   │   ├── Home.jsx  (Main feed page)
│   │   │   ├── Profile.jsx  (User profile page)
│   │   │   ├── EditProfile.jsx  (Edit profile page)
│   │   │   ├── Upload.jsx  (Upload Post, Loop or Story)
│   │   │   ├── Loops.jsx  (Short video feed)
│   │   │   ├── Story.jsx  (Story viewing page)
│   │   │   ├── Search.jsx  (Search users)
│   │   │   ├── Messages.jsx  (Chat list & online users)
│   │   │   ├── MessageArea.jsx  (One-to-one chat screen)
│   │   │   ├── Notifications.jsx  (Notifications page)
│   │   ├── 📂 hooks
│   │   │   ├── getCurrentUser.jsx  (Fetch logged-in user)
│   │   │   ├── getSuggestedUsers.jsx  (Fetch suggested users)
│   │   │   ├── getAllPost.jsx  (Fetch all posts)
│   │   │   ├── getAllLoops.jsx  (Fetch all Loops)
│   │   │   ├── getAllStories.jsx  (Fetch all Stories)
│   │   │   ├── getFollowingList.jsx  (Fetch following list)
│   │   │   ├── getPrevChatUsers.jsx  (Fetch previous chats)
│   │   │   ├── getAllNotifications.jsx  (Fetch notifications)
│   │   ├── 📂 redux
│   │   │   ├── store.js  (Redux store configuration)
│   │   │   ├── userSlice.js  (User, profile & notification state)
│   │   │   ├── postSlice.js  (Posts state)
│   │   │   ├── loopSlice.js  (Loops state)
│   │   │   ├── storySlice.js  (Stories state)
│   │   │   ├── messageSlice.js  (Chat messages state)
│   │   │   ├── socketSlice.js  (Socket instance & online users)
│
└── 📖 README.md  (Project documentation)
```

## 🚀 Features

- ✅ **Authentication:** Signup and signin with bcrypt-hashed passwords and JWT cookie sessions.
- ✅ **Password Reset with OTP:** A 4-digit OTP is sent by email and expires in 5 minutes.
- ✅ **Posts:** Upload images or videos with captions, like, comment, and save posts.
- ✅ **Loops:** Short video feed with likes and comments.
- ✅ **Stories:** Upload image or video Stories that auto-expire after 24 hours and show who viewed them.
- ✅ **Follow System:** Follow and unfollow users and get suggested users to follow.
- ✅ **User Search & Profiles:** Search users, view profiles, and edit your own profile with a photo, bio, profession, and gender.
- ✅ **Real-Time Chat:** One-to-one messaging with text and images, plus live online status.
- ✅ **Live Notifications:** Instant alerts for likes, comments, and new followers.
- ✅ **Live Counters:** Like and comment counts update in real time for everyone viewing the content.
- ✅ **Media Storage:** Images and videos are uploaded to Cloudinary.

## 🔧 Tech Stack

- **Frontend:** React.js, Redux Toolkit, React Router, TailwindCSS, Vite, React Icons, React Spinners
- **Backend:** Node.js, Express.js, Socket.IO
- **Database:** MongoDB with Mongoose
- **Authentication:** JWT, bcrypt.js, cookie-parser
- **Media Storage:** Cloudinary, Multer
- **Email:** Nodemailer (OTP emails)
- **HTTP Client:** Axios

## 📥 Installation & Setup

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/ravisainii701/NEXUS.git
cd NEXUS
```

### 2️⃣ Backend Setup

```bash
cd backend
npm install
```

### 3️⃣ Frontend Setup

```bash
cd frontend
npm install
```

### 4️⃣ Set Environment Variables

Create a `.env` file in the `backend` directory:

```env
PORT=8000
MONGODB_URL=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
EMAIL=your_email_address
EMAIL_PASS=your_email_app_password
```

> ⚠️ Keep `PORT=8000`. The frontend calls the API at `http://localhost:8000` (set in `frontend/src/App.jsx`), and the backend defaults to 5000 if `PORT` is not set.

## 📌 Steps to Run the Project

### 5️⃣ Run the Backend Server

```bash
cd backend
npm run dev
```

The API will be available at: http://localhost:8000

### 6️⃣ Run the Frontend

```bash
cd frontend
npm run dev
```

Frontend will be available at: http://localhost:5173

## 📡 API Endpoints

**Auth** (`/api/auth`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/signup` | Register a new user |
| POST | `/signin` | Log in a user |
| GET | `/signout` | Log out a user |
| POST | `/sendOtp` | Send OTP to email |
| POST | `/verifyOtp` | Verify OTP |
| POST | `/resetPassword` | Reset password |

**User** (`/api/user`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/current` | Get current logged-in user |
| GET | `/suggested` | Get suggested users |
| GET | `/getProfile/:userName` | Get a user's profile |
| GET | `/follow/:targetUserId` | Follow or unfollow a user |
| GET | `/followingList` | Get the following list |
| GET | `/search` | Search users |
| GET | `/getAllNotifications` | Get all notifications |
| POST | `/markAsRead` | Mark notifications as read |
| POST | `/editProfile` | Edit profile (with profile image) |

**Post** (`/api/post`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/upload` | Upload a post (image/video) |
| GET | `/getAll` | Get all posts |
| GET | `/like/:postId` | Like or unlike a post |
| GET | `/saved/:postId` | Save or unsave a post |
| POST | `/comment/:postId` | Comment on a post |

**Loop** (`/api/loop`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/upload` | Upload a Loop |
| GET | `/getAll` | Get all Loops |
| GET | `/like/:loopId` | Like or unlike a Loop |
| POST | `/comment/:loopId` | Comment on a Loop |

**Story** (`/api/story`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/upload` | Upload a Story |
| GET | `/getAll` | Get all Stories |
| GET | `/getByUserName/:userName` | Get a user's Story |
| GET | `/view/:storyId` | Mark a Story as viewed |

**Message** (`/api/message`)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/send/:receiverId` | Send a message (text/image) |
| GET | `/getAll/:receiverId` | Get chat history with a user |
| GET | `/prevChats` | Get previous chat users |

**Socket.IO Events**

| Event | Direction | Description |
|-------|-----------|-------------|
| `getOnlineUsers` | Server → Client | List of currently online users |
| `newMessage` | Server → Client | New chat message received |
| `newNotification` | Server → Client | New like, comment, or follow alert |
| `likedPost` / `commentedPost` | Server → Client | Live post like and comment updates |
| `likedLoop` / `commentedLoop` | Server → Client | Live Loop like and comment updates |

## 🚀 Deployment

### 🌍 Backend Deployment (Node.js/Express)

- Use Render, Railway, AWS EC2, or DigitalOcean to host the backend.
- Add a `"start": "node index.js"` script to `backend/package.json` (only `dev` exists right now).
- Set all environment variables in your hosting provider's dashboard.
- Replace the hardcoded `http://localhost:5173` in `backend/index.js` and `backend/socket.js` with your deployed frontend URL for CORS.
- Ensure MongoDB Atlas allows connections from your server's IP.

### 🖥 Frontend Deployment (React + Vite)

- Replace `serverUrl` in `frontend/src/App.jsx` with your deployed backend URL.

**Deploy on Vercel**

```bash
cd frontend
npm install -g vercel
vercel login
vercel deploy
```

**Deploy on Netlify**

```bash
cd frontend
npm install -g netlify-cli
netlify login
netlify deploy --prod
```

## 🌱 How It Works

1️⃣ A user signs up, signs in, and gets a secure JWT cookie session.
2️⃣ They set up a profile, follow suggested users, and see a feed of Stories and Posts.
3️⃣ They upload Posts, Loops, or Stories, and media is stored on Cloudinary.
4️⃣ Likes, comments, and follows trigger instant notifications through Socket.IO.
5️⃣ Users chat one-to-one in real time and can see who is online.

## 🛠 Future Roadmap

- 📱 Mobile app (React Native)
- 👥 Group chats and voice/video calls
- 🔍 Hashtags and trending content
- 🛡️ Content moderation and reporting tools

## 🤝 Real-World Use Cases

- 🧑‍🎨 **Creators:** Share photos, videos, and short Loops with followers.
- 👫 **Friends & Communities:** Stay connected with Stories and instant chat.
- 🎓 **Developers & Students:** A full-stack reference project covering auth, real-time sockets, and media uploads.

## 🤝 Contributing

We welcome contributions from the community! Feel free to:

- Fork the repository
- Create a pull request with your changes
- Report issues or suggest improvements

## 📜 License

This project currently has no license file. Add a LICENSE file (e.g. MIT) to clarify usage terms.

**🌐 Connect. Share. Chat. In Real Time! 🚀**
