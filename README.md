# Rate My Bite
https://project-9-client.vercel.app/

## 🍔 Overview
Rate My Bite is a Next.js web application where users can discover, post, and review street food spots. The platform features premium content for subscribed users, an admin dashboard for content moderation, and a comprehensive street food discovery experience.

## ✨ Features
- **User Authentication**
  - Register and login with email and password
  - JWT-based secure authentication
  - User profile management (update name, avatar, etc.)
- **Food Discovery**
  - Browse street food spots
  - Search by name, category, or location
  - Filter by price range, rating, and popularity
  - View detailed information about each food spot (images, reviews, location, price)
- **Content Creation**
  - Post new street food discoveries
  - Upload multiple images
  - Categorize and tag posts
  - Set price ranges and location information
- **Interaction**
  - Upvote/downvote food spots
  - Rate spots from 1-5 stars
  - Comment on posts
  - View user reviews and ratings
- **Premium Features**
  - Subscribe to access exclusive premium content
  - Integrated payment gateway (ShurjoPay/SSLCommerz)
  - Manage subscription status
- **Admin Dashboard**
  - Review and approve/reject pending posts
  - Mark content as premium/exclusive
  - Moderate comments and reviews
  - Manage users (ban, role change) and categories
- **Responsive Design**
  - Fully responsive UI for all devices
  - Mobile-first approach with Tailwind CSS

## 🛠️ Tech Stack
- **Framework**: Next.js (App Router)
- **Styling**: Tailwind CSS
- **Form Handling**: React Hook Form
- **Validation**: Zod
- **Authentication**: JWT (stored in HTTP-only cookies or localStorage)
- **Payment**: ShurjoPay / SSLCommerz
- **State Management**: Context API or Zustand (not specified)
- **Other**: TypeScript, Axios/Fetch for API calls

## 📂 Project Folder Structure
```text
project-9-client/
├── public/                  # Static assets
│   ├── images/
│   └── favicon.ico
├── src/
│   ├── app/                 # App Router (pages & layouts)
│   │   ├── api/             # (optional) Next.js API routes
│   │   ├── (auth)/          # Grouped auth routes
│   │   ├── posts/           # /posts & /posts/[id]
│   │   ├── profile/
│   │   ├── admin/           # Protected admin routes
│   │   ├── layout.tsx
│   │   ├── page.tsx         # Home
│   │   └── globals.css
│   ├── components/          # Reusable components
│   │   ├── ui/              # Button, Card, Modal, etc.
│   │   ├── layout/          # Navbar, Footer, Sidebar
│   │   ├── food/            # FoodSpotCard, FoodSpotDetail, RatingStars
│   │   ├── auth/            # LoginForm, RegisterForm
│   │   ├── admin/           # Admin tables, modals
│   │   └── premium/         # Premium badge, gated content
│   ├── lib/                 # Utilities
│   │   ├── auth.ts          # JWT & auth helpers
│   │   ├── api.ts           # API client (axios/fetch)
│   │   └── constants.ts
│   ├── types/               # TypeScript interfaces
│   │   ├── index.ts
│   │   ├── user.ts
│   │   ├── post.ts
│   │   └── ...
│   ├── hooks/               # Custom hooks (useAuth, usePayment, etc.)
│   └── models/              # Data model interfaces (optional)
├── .env.local               # Environment variables (gitignored)
├── next.config.ts
├── tailwind.config.js
├── tsconfig.json
├── package.json
└── README.md
```


## 📊 Data Models (TypeScript Interfaces)

```ts
// src/types/user.ts
export interface User {
  _id: string;
  name: string;
  email: string;
  role: 'user' | 'admin';
  avatar?: string;
  isPremium: boolean;
  subscription?: {
    status: 'active' | 'expired' | 'cancelled';
    expiryDate?: string;
  };
  createdAt: string;
}

// src/types/post.ts
export interface FoodSpot {
  _id: string;
  title: string;
  description: string;
  images: string[];           // Array of image URLs
  category: string;
  tags?: string[];
  priceRange: string;         // e.g. "10-50 TK"
  location: {
    city: string;
    area?: string;
    coordinates?: { lat: number; lng: number };
  };
  rating: number;             // Average rating (1-5)
  ratingsCount: number;
  upvotes: number;
  downvotes: number;
  isPremium: boolean;
  status: 'pending' | 'approved' | 'rejected';
  author: User | string;
  createdAt: string;
  updatedAt: string;
}

// src/types/review.ts
export interface Review {
  _id: string;
  postId: string;
  user: User | string;
  rating: number;             // 1-5
  comment: string;
  createdAt: string;
}

// src/types/category.ts
export interface Category {
  _id: string;
  name: string;
  description?: string;
  icon?: string;
}
