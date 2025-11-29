# Backend API

A comprehensive backend API built with Node.js, Express, and MongoDB, featuring video sharing, social interactions, and user management functionalities.

## Features

- **User Management**: Registration, login, profile management, and authentication
- **Video Management**: Upload, publish, update, and delete videos
- **Social Features**:
  - Tweet creation and management
  - Like/unlike videos, comments, and tweets
  - Subscribe/unsubscribe to channels
  - Comments on videos
- **Playlists**: Create and manage video playlists
- **Dashboard**: Channel statistics and analytics
- **Health Check**: API health monitoring endpoint

## Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js v5.1.0
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (JSON Web Tokens)
- **File Upload**: Multer & Cloudinary
- **Password Hashing**: Bcrypt
- **Environment Variables**: dotenv

## Prerequisites

- Node.js (v14 or higher)
- MongoDB
- Cloudinary account (for media storage)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file in the root directory:
```env
PORT=8000
MONGODB_URI=your_mongodb_connection_string
CORS_ORIGIN=*

ACCESS_TOKEN_SECRET=your_access_token_secret
ACCESS_TOKEN_EXPIRY=1d
REFRESH_TOKEN_SECRET=your_refresh_token_secret
REFRESH_TOKEN_EXPIRY=10d

CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
```

4. Start the development server:
```bash
npm run dev
```

The server will start at `http://localhost:8000`

## API Endpoints

### User Routes (`/api/v1/users`)
- `POST /register` - Register a new user
- `POST /login` - User login
- `POST /logout` - User logout (protected)
- `POST /refresh-token` - Refresh access token
- `POST /change-password` - Change password (protected)
- `GET /current-user` - Get current user details (protected)
- `PATCH /update-account` - Update account details (protected)
- `PATCH /avatar` - Update avatar (protected)
- `PATCH /cover-image` - Update cover image (protected)
- `GET /channel/:username` - Get user channel profile (protected)
- `GET /history` - Get watch history (protected)

### Video Routes (`/api/v1/videos`)
- `GET /` - Get all videos (protected)
- `POST /` - Publish a video (protected)
- `GET /:videoId` - Get video by ID (protected)
- `PATCH /:videoId` - Update video (protected)
- `DELETE /:videoId` - Delete video (protected)
- `PATCH /toggle/publish/:videoId` - Toggle publish status (protected)

### Tweet Routes (`/api/v1/tweets`)
- `POST /` - Create a tweet (protected)
- `GET /user/:userId` - Get user tweets (protected)
- `PATCH /:tweetId` - Update tweet (protected)
- `DELETE /:tweetId` - Delete tweet (protected)

### Comment Routes (`/api/v1/comments`)
- `GET /:videoId` - Get video comments (protected)
- `POST /:videoId` - Add comment to video (protected)
- `PATCH /c/:commentId` - Update comment (protected)
- `DELETE /c/:commentId` - Delete comment (protected)

### Like Routes (`/api/v1/likes`)
- `POST /toggle/v/:videoId` - Toggle like on video (protected)
- `POST /toggle/c/:commentId` - Toggle like on comment (protected)
- `POST /toggle/t/:tweetId` - Toggle like on tweet (protected)
- `GET /videos` - Get liked videos (protected)

### Playlist Routes (`/api/v1/playlists`)
- `POST /` - Create playlist (protected)
- `GET /:playlistId` - Get playlist by ID (protected)
- `PATCH /:playlistId` - Update playlist (protected)
- `DELETE /:playlistId` - Delete playlist (protected)
- `PATCH /add/:videoId/:playlistId` - Add video to playlist (protected)
- `PATCH /remove/:videoId/:playlistId` - Remove video from playlist (protected)
- `GET /user/:userId` - Get user playlists (protected)

### Subscription Routes (`/api/v1/subscriptions`)
- `POST /c/:channelId` - Toggle subscription (protected)
- `GET /c/:channelId` - Get channel subscribers (protected)
- `GET /u/:subscriberId` - Get subscribed channels (protected)

### Dashboard Routes (`/api/v1/dashboard`)
- `GET /stats` - Get channel statistics (protected)
- `GET /videos` - Get channel videos (protected)

### Health Check (`/api/v1/healthcheck`)
- `GET /` - Health check endpoint

## Project Structure

```
backend/
├── src/
│   ├── controllers/      # Request handlers
│   ├── models/          # Mongoose models
│   ├── routes/          # API routes
│   ├── middlewares/     # Custom middlewares
│   ├── utils/           # Utility functions
│   ├── app.js           # Express app configuration
│   └── index.js         # Application entry point
├── public/              # Static files
├── .env                 # Environment variables
├── .gitignore          # Git ignore rules
├── package.json        # Project dependencies
└── README.md           # Project documentation
```

## Models

- **User**: User authentication and profile
- **Video**: Video content and metadata
- **Tweet**: Social posts
- **Comment**: Video comments
- **Like**: Likes on videos, comments, and tweets
- **Playlist**: Video playlists
- **Subscription**: Channel subscriptions

## Middleware

- **verifyJWT**: Authentication middleware using JWT
- **upload**: File upload middleware using Multer

## Error Handling

The API uses custom error handling with the `ApiError` class and `asyncHandler` wrapper for consistent error responses.

## Response Format

All API responses follow a standard format using the `ApiResponse` class:

```json
{
  "statusCode": 200,
  "data": {},
  "message": "Success message",
  "success": true
}
```

## Development

- **Author**: Akash Rajput
- **License**: ISC
- **Version**: 1.0.0

### Scripts

- `npm run dev` - Start development server with nodemon

## Dependencies

- `express` - Web framework
- `mongoose` - MongoDB ODM
- `mongoose-aggregate-paginate-v2` - Pagination plugin
- `bcrypt` - Password hashing
- `jsonwebtoken` - JWT authentication
- `multer` - File upload handling
- `cloudinary` - Cloud storage for media
- `cookie-parser` - Parse cookies
- `cors` - Cross-origin resource sharing
- `dotenv` - Environment variable management

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

ISC
