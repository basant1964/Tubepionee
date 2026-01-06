# Tubepionee
tubepionee pi browser me youtube ke jaisa same project hai, ye project mit license ke under licensed hai. is project ko freely use, modify aur distribute kiya ja sakta hai. bas original copyright aur licens notice ka mention karna zaruri hai, license alag se hai.
Full TubePioneE structure:

TubePioneE/
│
├── backend/
│   ├── server.js
│   ├── package.json
│   ├── config/
│   │   └── db.js
│   ├── models/
│   │   ├── User.js
│   │   └── Video.js
│   ├── routes/
│   │   ├── auth.js
│   │   └── videos.js
│   └── middleware/
│       └── auth.js
│
└── frontend/
    ├── index.html
    ├── upload.html
    ├── css/style.css
    └── js/app.js
{
  "name": "tubepionee",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": { "start": "node server.js" },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.6.0",
    "jsonwebtoken": "^9.0.2",
    "cors": "^2.8.5",
    "multer": "^1.4.5"
  }
}
const mongoose = require('mongoose');

module.exports = () => {
  mongoose.connect('mongodb://127.0.0.1:27017/tubepionee')
    .then(() => console.log('MongoDB Connected'))
    .catch(err => console.log(err));
};
const mongoose = require('mongoose');

const UserSchema = new mongoose.Schema({
  username: String,
  wallet: String
});

module.exports = mongoose.model('User', UserSchema);
const mongoose = require('mongoose');

const VideoSchema = new mongoose.Schema({
  title: String,
  filename: String,
  views: { type: Number, default: 0 },
  createdAt: { type: Date, default: Date.now }
});

module.exports = mongoose.model('Video', VideoSchema);
const express = require('express');
const multer = require('multer');
const Video = require('../models/Video');

const router = express.Router();

const storage = multer.diskStorage({
  destination: 'uploads/',
  filename: (req, file, cb) => cb(null, Date.now() + file.originalname)
});