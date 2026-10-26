# Kapilmuni Online Blood — সেটআপ গাইড

ফাইলগুলো:
- `index.html` — ইউজার অ্যাপ/ওয়েবসাইট
- `admin.html` — অ্যাডমিন প্যানেল (ওয়েবসাইটে `/admin` লিংকে খুলবে)
- `firestore.rules` — ডাটাবেজের সুরক্ষা রুলস
- `vercel.json`, `manifest.webmanifest`, `sw.js`, `icon-*.png` — Vercel ও "অ্যাপ হিসেবে ইনস্টল" এর জন্য

## ধাপ ১ — Firebase Authentication
Firebase Console → **Authentication → Sign-in method** → **Email/Password** চালু করুন (Google/Phone আগে চালু থাকলে থাকুক)।

## ধাপ ২ — Firestore rules
Firebase Console → **Firestore Database → Rules** → `firestore.rules` ফাইলের পুরো লেখা পেস্ট করে **Publish**।

## ধাপ ৩ — অ্যাডমিন অ্যাকাউন্ট (খুব গুরুত্বপূর্ণ)
Firebase Console → **Authentication → Users → Add user**
- Email: `admin@kapilmuni.app`
- Password: আপনার নিজের শক্ত পাসওয়ার্ড (এটাই অ্যাডমিন প্যানেলের পাসওয়ার্ড)

এই কাজ সাইট চালু করার **আগেই** করুন, যাতে অন্য কেউ ওই ইমেইলে অ্যাকাউন্ট খুলতে না পারে।
অন্য ইমেইল চাইলে `admin.html`-এর `ADMIN_EMAIL` এবং `firestore.rules`-এর `isAdmin()` — দুই জায়গাতেই বদলান।

## ধাপ ৪ — GitHub ও Vercel
1. GitHub-এ নতুন repository খুলে এই ফোল্ডারের সব ফাইল আপলোড করুন।
2. vercel.com → **Add New Project** → repository সিলেক্ট → **Deploy** (কোনো build সেটিং লাগবে না)।
3. Vercel-এর ডোমেইন (যেমন `yourapp.vercel.app`) Firebase Console → **Authentication → Settings → Authorized domains**-এ যোগ করুন। না করলে লগইন কাজ করবে না।

## ধাপ ৫ — ব্যবহার
- ইউজার: `https://yourapp.vercel.app`
- অ্যাডমিন: `https://yourapp.vercel.app/admin`
- ফোনে Chrome-এ সাইট খুলে **Add to Home screen / Install app** দিলে অ্যাপের মতো চলবে।

## অ্যাডমিন প্যানেলের মেনু
Dashboard · Notice bar · All-member notice · Slider banners · Community · Urgent requests · Donations · Members · ID card requests · Reports · Site settings · Live activity · Chats & Online

## আইডি কার্ড কীভাবে কাজ করে
- ২ বার রক্তদান হলে কার্ড নিজে থেকে খুলে যায়।
- না হলে ইউজার কার্ড স্ক্রিনে কারণ লিখে অ্যাডমিনের কাছে আবেদন করে।
- অ্যাডমিন **ID card requests**-এ তথ্য যাচাই করে Approve করলে ইউজারের কার্ড সাথে সাথে খুলে যায়; Reject করলে নির্বাচিত কারণ ইউজার দেখে।

## মনে রাখবেন
- Firebase `apiKey` ওয়েব কোডে থাকা স্বাভাবিক; সুরক্ষা আসে `firestore.rules` থেকে।
- অ্যাডমিন ও ইউজার অ্যাপ একই ডোমেইনে হলে একই ব্রাউজারে দুটোতে একসাথে লগইন থাকে না। অ্যাডমিন প্যানেল আলাদা ব্রাউজার/প্রোফাইলে খুলুন।
- ভয়েস কল WebRTC দিয়ে চলে। মোবাইল ডেটায় কল না লাগলে `index.html`-এ TURN সার্ভার যোগ করতে হবে।
