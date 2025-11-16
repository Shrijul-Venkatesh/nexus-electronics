# Nexus Electronics

A production-ready full-stack MERN e-commerce platform featuring AI-powered product recommendations using vector similarity search. Built with React, Node.js, Express, MongoDB, and integrated with Pinecone for intelligent product recommendations.

## 🚀 Features

- **E-Commerce Core**
  - Product browsing and search
  - Shopping cart with persistent storage
  - Secure checkout flow with payment validation
  - User authentication (register, login, password reset)
  - Order tracking with real-time status updates

- **AI-Powered Recommendations**
  - Vector-based product similarity search using Pinecone
  - Semantic search powered by Google Generative AI embeddings
  - Automatic product synchronization to vector database
  - Fallback heuristic scoring when vector search is unavailable

- **Modern UI/UX**
  - Responsive Material-UI design
  - Real-time search with instant results
  - Product carousels and featured sections
  - Smooth animations and transitions

- **Developer Experience**
  - Comprehensive API documentation (Swagger UI)
  - Full test coverage (Jest + React Testing Library)
  - Docker support for containerized deployment
  - Kubernetes and Nomad deployment configurations

## 🛠️ Tech Stack

### Frontend
- **React 18** with React Router v6
- **Material-UI (MUI)** for component library
- **Axios** with exponential backoff retry logic
- **React Context API** for state management

### Backend
- **Node.js** with Express.js
- **MongoDB** with Mongoose ODM
- **JWT** for authentication
- **Swagger/OpenAPI** for API documentation

### AI & Vector Search
- **Pinecone** (primary vector database)
- **Google Generative AI** for text embeddings
- **Weaviate** (optional alternative vector DB)
- **FAISS** (optional local vector search)

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher)
- **npm** (v9 or higher)
- **MongoDB** (local instance or MongoDB Atlas account)
- **Pinecone account** (for AI recommendations)
- **Google AI API key** (for generating embeddings)

## 🔧 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/hoangsonww/MERN-Stack-Ecommerce-App.git
cd MERN-Stack-Ecommerce-App
```

### 2. Install Frontend Dependencies

```bash
npm install
```

### 3. Install Backend Dependencies

```bash
cd backend
npm install
cd ..
```

### 4. Configure Environment Variables

Create a `.env` file in the `backend/` directory:

```env
# Database
MONGO_URI=mongodb://localhost:27017/Ecommerce-Products

# Authentication
JWT_SECRET=your_super_secret_jwt_key_here

# Pinecone (Vector Database)
PINECONE_API_KEY=your_pinecone_api_key
PINECONE_HOST=https://your-index.svc.us-east-1.pinecone.io
PINECONE_INDEX=ecommerce-products
PINECONE_NAMESPACE=ecommerce-products

# Google AI (for embeddings)
GOOGLE_AI_API_KEY=your_google_ai_api_key

# Optional: Server Configuration
PORT=5000
SKIP_SEED_ON_START=false
FORCE_SEED_ON_START=false
```

### 5. Seed the Database

```bash
cd backend
npm run seed
```

This will populate your MongoDB database with sample products.

### 6. Sync Vector Database

Sync products to Pinecone for AI-powered recommendations:

```bash
cd backend
npm run sync-pinecone
```

This process:
- Generates embeddings for all products using Google AI
- Uploads vectors to Pinecone
- Enables semantic product similarity search

## 🎯 Usage

### Development Mode

Run both frontend and backend concurrently:

```bash
npm run dev
```

This starts:
- **Frontend** on `http://localhost:3000`
- **Backend** on `http://localhost:5000` (or your configured PORT)

### Run Separately

**Frontend only:**
```bash
npm start
```

**Backend only:**
```bash
cd backend && npm start
```

### Access Points

- **Frontend Application**: http://localhost:3000
- **Backend API**: http://localhost:5000
- **API Documentation (Swagger)**: http://localhost:5000/api-docs

## 🧪 Testing

### Frontend Tests

```bash
# Run all tests
npm test

# Watch mode
npm run test:watch

# With coverage
npm run test:coverage
```

### Backend Tests

```bash
cd backend

# Run all tests
npm test

# Watch mode
npm run test:watch

# With coverage
npm run test:coverage
```

## 📚 API Endpoints

### Products
- `GET /api/products` - Get all products
- `GET /api/products/:id` - Get product by ID
- `GET /api/products/:id/similar` - Get similar products (AI-powered)
- `GET /api/products/category/:category` - Get products by category
- `PUT /api/products/:id/rating` - Update product rating

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login
- `POST /api/auth/verify-email` - Verify email for password reset
- `POST /api/auth/reset-password` - Reset user password

### Search
- `GET /api/search?q=query` - Search products by name/description

### Checkout
- `POST /api/checkout/create-order` - Create new order

### Orders
- `GET /api/orders/:orderNumber` - Get order details
- `GET /api/orders` - Get all orders (requires auth)

Full API documentation is available at `/api-docs` when the backend is running.

## 🔄 Vector Database Operations

### Pinecone (Primary)

```bash
cd backend

# Full sync: MongoDB → Pinecone
npm run sync-pinecone
```

### Weaviate (Optional)

```bash
# Initial upsert
npm run weaviate-upsert

# Sync IDs
npm run sync-weaviate

# Query test
npm run weaviate-query
```

### FAISS (Optional, Local)

```bash
# Build index
npm run faiss-upsert

# Search with query
npm run faiss-search -- "your search query" 5
```

## 🏗️ Project Structure

```
nexus-electronics/
├── backend/                 # Express.js backend
│   ├── routes/             # API route handlers
│   ├── models/             # Mongoose models
│   ├── services/           # Business logic (Pinecone sync, etc.)
│   ├── middleware/         # Express middleware
│   ├── scripts/           # Utility scripts
│   └── seed/              # Database seeding
├── src/                    # React frontend
│   ├── components/         # Reusable React components
│   ├── pages/              # Page components
│   ├── services/           # API client utilities
│   └── context/            # React Context providers
├── public/                 # Static assets
└── docs/                   # Documentation
```

## 🐳 Docker Deployment

Build and run with Docker Compose:

```bash
docker compose up --build
```

This will:
- Build frontend and backend containers
- Set up nginx reverse proxy
- Expose the application on port 80

## 🔐 Security Notes

- **JWT_SECRET**: Use a strong, random secret in production
- **API Keys**: Never commit `.env` files to version control
- **CORS**: Configure allowed origins for production
- **Rate Limiting**: Consider adding rate limiting for production use

## 🚢 Deployment

The application is configured for deployment on:

- **Frontend**: Vercel (automatic builds on push)
- **Backend**: Vercel (serverless) or Render (Docker)
- **Database**: MongoDB Atlas
- **Vector DB**: Pinecone Serverless

See `CLAUDE.md` for detailed deployment architecture.

## 📖 Additional Documentation

- **CLAUDE.md** - Comprehensive development guide and architecture details
- **ARCHITECTURE.md** - System design and data flow documentation
- **AGENTS.md** - AI agent instructions and task examples

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Son Nguyen**

- GitHub: [@hoangsonww](https://github.com/hoangsonww)
- Email: hoangson091104@gmail.com

## 🙏 Acknowledgments

- Material-UI for the component library
- Pinecone for vector database infrastructure
- Google AI for embedding generation
- MongoDB for database solutions

---

**Note**: This is a demo/portfolio project. The checkout flow is simulated and does not process real payments. Orders are not persisted to the database in the current implementation.
