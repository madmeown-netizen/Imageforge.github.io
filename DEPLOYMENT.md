# Deployment Guide for ImageForge

This guide covers different deployment options for the ImageForge application.

## Quick Deploy Options

### 1. Vercel (Recommended)

1. **Fork/Clone the repository to your GitHub account**
2. **Connect to Vercel**:
   - Go to [vercel.com](https://vercel.com)
   - Import your GitHub repository
   - Vercel will auto-detect the Vite configuration

3. **Configure Environment Variables**:
   ```
   NODE_ENV=production
   ```

4. **Deploy**: Vercel will automatically build and deploy your application

### 2. Netlify

1. **Connect your GitHub repository to Netlify**
2. **Build settings**:
   - Build command: `npm run build`
   - Publish directory: `dist/public`
3. **Deploy**: Netlify will handle the rest

### 3. Railway

1. **Connect to Railway**:
   - Go to [railway.app](https://railway.app)
   - Connect your GitHub repository
   
2. **Configure**:
   - Railway will auto-detect Node.js
   - Set environment variables as needed

3. **Deploy**: Railway will build and deploy automatically

## Self-Hosted Deployment

### Docker Deployment

1. **Build the Docker image**:
   ```bash
   docker build -t imageforge .
   ```

2. **Run the container**:
   ```bash
   docker run -p 5000:5000 imageforge
   ```

3. **Or use Docker Compose**:
   ```bash
   docker-compose up -d
   ```

### Manual Server Deployment

1. **Install Node.js 18+ on your server**

2. **Clone and build the application**:
   ```bash
   git clone https://github.com/yourusername/imageforge.git
   cd imageforge
   npm install
   npm run build
   ```

3. **Start the application**:
   ```bash
   npm start
   ```

4. **Use a process manager** (PM2 recommended):
   ```bash
   npm install -g pm2
   pm2 start dist/index.js --name imageforge
   pm2 startup
   pm2 save
   ```

5. **Set up reverse proxy** (Nginx example):
   ```nginx
   server {
       listen 80;
       server_name yourdomain.com;
       
       location / {
           proxy_pass http://localhost:5000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

## Environment Variables

For production deployments, set these environment variables:

```env
NODE_ENV=production
PORT=5000
DATABASE_URL=your_database_url_here  # Optional
```

## Database Setup (Optional)

The application uses in-memory storage by default. For production with persistent data:

1. **Set up PostgreSQL database**
2. **Update DATABASE_URL environment variable**
3. **Run database migrations**:
   ```bash
   npm run db:push
   ```

## Performance Considerations

### File Storage
- For production, consider using cloud storage (AWS S3, Google Cloud Storage)
- Configure CDN for serving converted images
- Implement cleanup jobs for temporary files

### Scaling
- Use Redis for session storage in multi-instance deployments
- Implement queue system for image processing jobs
- Consider using dedicated image processing workers

### Monitoring
- Set up application monitoring (e.g., Sentry for error tracking)
- Monitor file system usage for uploads/output directories
- Set up health checks for load balancers

## Security Considerations

1. **File Upload Security**:
   - Validate file types and sizes
   - Scan uploaded files for malware
   - Implement rate limiting

2. **API Security**:
   - Add authentication for production use
   - Implement CORS policies
   - Use HTTPS in production

3. **Server Security**:
   - Keep dependencies updated
   - Use security headers
   - Regular security audits

## Troubleshooting

### Common Issues

1. **Sharp installation issues**:
   ```bash
   npm rebuild sharp
   ```

2. **Memory issues with large images**:
   - Increase Node.js memory limit: `--max-old-space-size=4096`
   - Implement image preprocessing to limit sizes

3. **File permission issues**:
   ```bash
   chmod 755 uploads output
   ```

### Health Checks

The application includes a health check endpoint:
```bash
curl http://localhost:5000/health
```

### Logs

Check application logs for debugging:
```bash
# PM2 logs
pm2 logs imageforge

# Docker logs
docker logs container_name
```

## Backup and Recovery

1. **Database backups** (if using PostgreSQL):
   ```bash
   pg_dump -h hostname -U username database_name > backup.sql
   ```

2. **File system backups**:
   - Regular backups of uploads and output directories
   - Consider automated backup solutions

## Updates and Maintenance

1. **Update dependencies**:
   ```bash
   npm audit fix
   npm update
   ```

2. **Application updates**:
   ```bash
   git pull origin main
   npm install
   npm run build
   pm2 restart imageforge
   ```

3. **Database migrations**:
   ```bash
   npm run db:push
   ```

For specific deployment platform questions, refer to their respective documentation or contact support.