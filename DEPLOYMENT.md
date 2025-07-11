# Vercel Deployment Guide

## Prerequisites

1. **MongoDB Atlas**: You need a cloud MongoDB database (MongoDB Atlas recommended)
2. **Environment Variables**: Set up your environment variables in Vercel dashboard

## Environment Variables to Set in Vercel

Go to your Vercel project dashboard → Settings → Environment Variables and add:

```
DATABASE_URL=mongodb+srv://username:password@cluster.mongodb.net/database?retryWrites=true&w=majority
NODE_ENV=production
JWT_EXPIRES_IN=1d
LOG_LEVEL=info
MAX_FILE_SIZE=5242880
MAX_FILES=5
```

## CORS Configuration

Update the CORS origins in `index.ts` to match your frontend domain:

```javascript
origin: process.env.NODE_ENV === "production"
  ? ["https://your-frontend-domain.vercel.app", "https://your-custom-domain.com"]
  : ["http://localhost:5173", "http://localhost:3000"],
```

## Deployment Steps

1. Push your code to GitHub
2. Connect your GitHub repository to Vercel
3. Set the environment variables in Vercel dashboard
4. Deploy!

## Important Notes

- File uploads might not work as expected on Vercel due to serverless limitations
- Consider using cloud storage (AWS S3, Cloudinary) for file uploads in production
- Static files are served from `/public` and `/uploads` directories

## Testing

After deployment, test these endpoints:

- `https://your-app.vercel.app/test` - Should return API working message
- `https://your-app.vercel.app/api-docs` - Swagger documentation
- `https://your-app.vercel.app/` - Should redirect to custom Swagger UI

## Troubleshooting

If you get 404 errors:

1. Check that `vercel.json` is in the root directory
2. Verify environment variables are set correctly
3. Check MongoDB connection string
4. Review Vercel function logs in the dashboard
