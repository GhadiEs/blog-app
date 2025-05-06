# Blog App

This is a MERN stack blog application for posting blogs with image uploads.

## Technologies Used

- Frontend: React (Vite)
- Backend: Node.js + Express
- Database: MongoDB Atlas
- File Storage: AWS S3
- Hosting: EC2 (backend), S3 (frontend)

## Features

- User registration and login with JWT
- Create, update, delete blog posts
- Image upload to S3
- Posts are visible publicly
- Pagination

## .env Files

You need two `.env` files:

### backend/.env

```
PORT=5000
HOST=0.0.0.0
MODE=production
MONGODB=your_mongo_connection
JWT_SECRET=your_secret
JWT_REFRESH=your_refresh_token
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret_key
S3_BUCKET=ghadi-blogapp-media
MEDIA_BASE_URL=https://ghadi-blogapp-media.eu-north-1.amazonaws.com
```

### frontend/.env

```
VITE_BASE_URL=http://ec2-16-16-98-137.eu-north-1.compute.amazonaws.com:5000/api
VITE_MEDIA_BASE_URL=https://ghadi-blogapp-media.s3.eu-north-1.amazonaws.com
```

## Deployment Steps

### 1. MongoDB Atlas

- Create a cluster
- Add a database user
- Whitelist EC2 IP
- Get connection string

### 2. S3 Buckets

- Create one for frontend (static website)
- Create one for media uploads
- Enable public access
- Set CORS and Bucket Policy

### 3. EC2 Instance

- Create Ubuntu instance
- Allow ports 22, 80, 443, 5000
- SSH into EC2
- Install Node, NPM, PM2, Git, etc.

### 4. Clone and Run

```
git clone https://github.com/cw-barry/blog-app-MERN.git /home/ubuntu/blog-app
cd blog-app/backend
npm install
pm2 start index.js --name blog-backend
pm2 save
```

### 5. Build and Upload Frontend

```
cd blog-app/frontend
pnpm install
pnpm run build
aws s3 sync dist/ s3://ghadi-blogapp-frontend-bucket-name
```

## Notes

- Uploaded images go to the S3 media bucket
- Frontend is accessed via S3 static website URL
- Backend runs on EC2 public DNS at port 5000

## Screenshots

1- [Screenshot of backend server running]
2- [Screenshot of frontend s3 web page]
3- [Screenshot of file upload and retrieving a file]
4- [Screenshot of S3 public URL loading index.html]
5- ![curl -I output showing 200 OK]
6- ![full MERN functionality]
