# ImageForge - Professional Image Conversion Platform

A modern, full-stack SaaS web application for professional image conversion and optimization. Built with React, TypeScript, Node.js, and Sharp for high-performance image processing.

## Features

### 🚀 Core Functionality
- **Multi-format Support**: JPEG, PNG, WebP, GIF, BMP, TIFF input and output formats
- **Advanced Image Processing**: Powered by Sharp library for high-performance conversion
- **Quality Control**: Adjustable quality settings (1-100%) with real-time preview
- **Smart Resizing**: Multiple preset options and custom dimensions
- **File Size Targeting**: Automatically adjust compression to hit target file sizes
- **Batch Processing**: Convert multiple images simultaneously

### 🎨 User Experience
- **Drag & Drop Upload**: Intuitive file upload with progress indicators
- **Live Preview**: Thumbnail previews of uploaded images
- **Modern UI**: Clean, responsive design with Tailwind CSS and Shadcn/ui components
- **Real-time Status**: Track conversion progress with visual indicators
- **Bulk Download**: Download individual files or create ZIP archives

### ⚡ Technical Highlights
- **TypeScript**: Full type safety across frontend and backend
- **Real-time Processing**: Asynchronous image conversion with status tracking
- **RESTful API**: Clean, well-documented API endpoints
- **Responsive Design**: Mobile-first design that works on all devices
- **Memory Storage**: Fast in-memory storage for development (easily replaceable with database)

## Tech Stack

### Frontend
- **React 18** with TypeScript
- **Vite** for fast development and building
- **Tailwind CSS** for styling
- **Shadcn/ui** component library
- **TanStack Query** for server state management
- **React Dropzone** for file uploads
- **Wouter** for routing

### Backend
- **Node.js** with Express
- **TypeScript** for type safety
- **Sharp** for image processing
- **Multer** for file upload handling
- **Archiver** for ZIP file creation
- **Drizzle ORM** for database operations

## Quick Start

### Prerequisites
- Node.js 18 or higher
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/imageforge.git
   cd imageforge
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   Navigate to `http://localhost:5000`

## API Documentation

### Upload Images
```bash
POST /api/images/upload
Content-Type: multipart/form-data

# Upload multiple images
curl -X POST http://localhost:5000/api/images/upload \
  -F "images=@image1.jpg" \
  -F "images=@image2.png"
```

### Convert Images
```bash
POST /api/images/convert
Content-Type: application/json

{
  "imageIds": [1, 2, 3],
  "settings": {
    "outputFormat": "webp",
    "quality": 85,
    "resizePreset": "instagram-post",
    "targetFileSize": 1.5
  }
}
```

### Download Converted Image
```bash
GET /api/conversions/{id}/download
```

### Download as ZIP
```bash
POST /api/conversions/download-zip
Content-Type: application/json

{
  "conversionIds": [1, 2, 3]
}
```

## Configuration

### Environment Variables
```env
NODE_ENV=development
PORT=5000
DATABASE_URL=postgresql://user:password@localhost:5432/imageforge
```

### Supported Formats
- **Input**: JPEG, JPG, PNG, WebP, GIF, BMP, TIFF
- **Output**: JPEG, PNG, WebP, GIF, TIFF

### Size Presets
- **Thumbnail**: 150x150px
- **Instagram Post**: 1080x1080px
- **Facebook Cover**: 1200x630px
- **Twitter Header**: 1500x500px
- **Custom**: User-defined dimensions

## Project Structure

```
imageforge/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/     # UI components
│   │   ├── pages/          # Page components
│   │   ├── lib/            # Utility functions
│   │   └── hooks/          # Custom React hooks
│   └── index.html
├── server/                 # Express backend
│   ├── index.ts           # Server entry point
│   ├── routes.ts          # API routes
│   ├── storage.ts         # Data storage interface
│   └── vite.ts            # Vite integration
├── shared/                 # Shared types and schemas
│   └── schema.ts          # Database schema and validation
└── package.json
```

## Development

### Available Scripts
```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
npm run type-check   # Run TypeScript type checking
```

### Adding New Features

1. **Database Changes**: Update `shared/schema.ts`
2. **API Endpoints**: Add routes in `server/routes.ts`
3. **UI Components**: Create components in `client/src/components/`
4. **Pages**: Add pages in `client/src/pages/`

## Deployment

### Production Build
```bash
npm run build
npm start
```

### Docker Deployment
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 5000
CMD ["npm", "start"]
```

### Vercel/Netlify
The application is configured for easy deployment on modern hosting platforms. The build outputs static files that can be served by any web server.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- 📧 Email: support@imageforge.com
- 🐛 Issues: [GitHub Issues](https://github.com/yourusername/imageforge/issues)
- 📖 Documentation: [Wiki](https://github.com/yourusername/imageforge/wiki)

## Roadmap

- [ ] User authentication and accounts
- [ ] Cloud storage integration (AWS S3, Google Cloud)
- [ ] Advanced image filters and effects
- [ ] API rate limiting and usage analytics
- [ ] Webhook support for automated workflows
- [ ] Mobile app (React Native)

---

Built with ❤️ for the creative community