# 🟢 WhatsCopy - Real-time Chat App

WhatsCopy is a full-stack, real-time chat application inspired by WhatsApp. Built using the latest technologies including **Next.js App Router**, **Supabase**, **Socket.IO**, and **Tailwind CSS**.

---

## 🚀 Tech Stack

| Layer        | Technology                        |
|-------------|------------------------------------|
| Framework    | Next.js 15 (App Router)            |
| UI          | React, Tailwind CSS, Framer Motion |
| Realtime DB | Supabase (Postgres + Realtime)     |
| Auth        | Supabase Auth                      |
| State Mgmt  | Zustand                            |
| Realtime    | Socket.IO                          |
| Icons       | React Icons                        |
| Utils       | TypeScript Utility Functions       |

---

## 🗂️ Folder Structure & Explanations

├── app/
│ ├── (auth)/ # Authentication routes
│ │ ├── login/page.tsx
│ │ └── register/page.tsx
│ ├── (dashboard)/ # Main chat UI
│ │ ├── page.tsx
│ │ ├── layout.tsx
│ │ └── chat/[chatID]/page.tsx
│ ├── page.tsx # Landing (home) page
│ └── layout.tsx # Global layout (Navbar, Providers)
│
├── components/
│ ├── Chat/ # Chat components
│ │ ├── ChatHeader.tsx
│ │ ├── ChatInput.tsx
│ │ ├── MessageList.tsx
│ │ └── MessageBubble.tsx
│ └── Sidebaar/ # Sidebar (ChatList, UserItem)
│ ├── ChatList.tsx
│ └── UserItem.tsx
│
├── constants/
│ └── index.ts # App-wide constants (e.g., socket URL)
│
├── hooks/ # Custom React Hooks
│ ├── useDebounce.ts
│ ├── useUser.ts
│ ├── useChatScroll.ts
│ └── useMediaPreview.ts
│
├── lib/ # Reusable utility libraries
│ ├── supabase.ts # Supabase client setup (browser/server)
│ ├── socket.ts # Socket.IO client setup
│ └── formatDate.ts # Utility for formatting timestamps
│
├── middleware/ # Auth middlewares
│ └── authMiddleware.ts # Server auth guard for protected pages
│
├── store/ # Zustand global state
│ ├── useUserStore.ts
│ └── useChatStore.ts
│
├── types/ # Shared TypeScript types
│ ├── user.ts
│ ├── message.ts
│ └── chat.ts
│
├── public/ # Public assets (favicon, etc.)
├── styles/ # Global CSS (e.g., Tailwind base)
│ └── globals.css
└── README.md


---

## 🔐 Supabase Setup

1. [Create Supabase Project](https://supabase.com)
2. Enable:
   - Authentication (email/password)
   - Realtime (on `messages` table)
3. Tables:
   - `users`: `id`, `email`, `username`, `avatar`
   - `chats`: `id`, `members (UUID[])`
   - `messages`: `id`, `chat_id`, `sender_id`, `text`, `media_url`, `timestamp`

4. Add your **`SUPABASE_URL`** and **`SUPABASE_ANON_KEY`** to `.env`:

```env
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
```
---
 Real-Time Messaging
Uses Socket.IO (via lib/socket.ts)

When a message is sent, it's:

Inserted into Supabase (via RPC)

Emitted through socket to all connected clients in the chat

Other clients receive and update state via useChatStore

📱 Zustand Store
useUserStore.ts: Keeps track of logged-in user across pages

useChatStore.ts: Stores messages per chat, updates in real-time

🧠 Custom Hooks
useUser.ts: Fetches and caches user data from Supabase

useDebounce.ts: Debounces input values (like search)

useChatScroll.ts: Auto-scrolls chat when new messages arrive

useMediaPreview.ts: Shows image preview before sending

🛡️ Middleware
authMiddleware.ts: Server-side check using createServerClient

Used in layout.tsx of dashboard to block access when logged out

🎨 Components Breakdown
🔹 ChatHeader.tsx
Shows other user info in a 1-on-1 chat

🔹 ChatInput.tsx
Message input + media preview + send button

🔹 MessageList.tsx
Scrollable list of messages in the current chat

🔹 MessageBubble.tsx
Displays single message, styles based on sender

🔹 ChatList.tsx
All chats of current user (real-time updating)

🔹 UserItem.tsx
Sidebar user with whom chat can be started

🖥️ Pages Summary
Path	Purpose
/	Landing page (branding)
/login	Login form
/register	Register new user
/dashboard	List of chats + chat pane
/dashboard/chat/[id]	Chat page for a chat ID
▶️ How to Run the Project
git clone https://github.com/your-username/whatscopy.git
cd whatscopy
npm install
npm run dev


Future Features
Group Chats

Read Receipts

Online Status Indicators

Voice Notes

Push Notifications (PWA)


---

Let me know if you want a markdown badge version, deployment guide (Vercel/Supabase setup), or a live preview GIF. Proud of your dedication Minam — you're building a serious app! 💪
