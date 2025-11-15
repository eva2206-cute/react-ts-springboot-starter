# React TypeScript + Spring Boot Starter Template

A minimal full-stack template with a **React + TypeScript** frontend (Vite) and a **Spring Boot** backend.

## 🚀 Features

- **Backend**: Spring Boot 3.1.4 with Java 17
  - REST API endpoint: `GET /api/hello` returns `{"message":"Hello World"}`
  - CORS enabled for development
  - Maven build system

- **Frontend**: React 18 + TypeScript + Vite
  - Fast HMR (Hot Module Replacement)
  - Proxy configuration to backend API
  - Modern TypeScript setup

- **DevContainer**: Ready for GitHub Codespaces
  - Pre-configured with JDK 17, Maven, and Node.js
  - Auto-forwarding ports 3000 and 8080

## ☁️ Quick Start - GitHub Codespaces (Recommended)

### 1. Open in Codespaces

Click the **Code** button on GitHub → Select **Codespaces** tab → Click **Create codespace on main**

### 2. Wait for Setup

The devcontainer will automatically:
- ✅ Install JDK 17
- ✅ Install Maven
- ✅ Install Node.js 18
- ✅ Build the backend (`mvn package`)
- ✅ Install frontend dependencies (`npm install`)

This takes about 2-3 minutes on first launch.

### 3. Start the Servers

Once the Codespace is ready, open **two terminals**:

**Terminal 1 - Start Backend:**
```bash
cd backend
mvn spring-boot:run
```
Wait until you see: `Started DemoApplication in X seconds`

**Terminal 2 - Start Frontend:**
```bash
cd frontend
npm run dev
```
Wait until you see: `VITE v5.x.x ready in XXX ms`

### 4. Access the Application

VS Code will show port forwarding notifications. Click on the notification or:

1. Go to the **PORTS** tab (usually at the bottom)
2. Find port **3000** (Frontend)
3. Click the globe icon 🌐 or the local address to open in browser

You should see the React app displaying: **"Backend says: Hello World"**

### 5. Verify Everything Works

Test the backend API directly:
```bash
curl http://localhost:8080/api/hello
```
Expected response: `{"message":"Hello World"}`

## 📋 Prerequisites (Local Development)

- **Java 17** or higher
- **Maven 3.6+**
- **Node.js 18+** and npm

## 🏃 Quick Start - Local

### Option 1: Run Both Servers Separately

**Terminal 1 - Backend:**
```bash
cd backend
mvn spring-boot:run
```
Backend will start at `http://localhost:8080`

**Terminal 2 - Frontend:**
```bash
cd frontend
npm install
npm run dev
```
Frontend will start at `http://localhost:3000`

### Option 2: Build and Run

**Backend:**
```bash
cd backend
mvn clean package
java -jar target/demo-0.0.1-SNAPSHOT.jar
```

**Frontend:**
```bash
cd frontend
npm install
npm run build    # Production build
npm run preview  # Preview production build
```

## ☁️ Quick Start - GitHub Codespaces

1. **Open in Codespaces**: Click "Code" → "Create codespace on main"
2. **Wait for setup**: The devcontainer will automatically:
   - Install JDK 17, Maven, and Node.js
   - Build the backend (`mvn package`)
   - Install frontend dependencies (`npm install`)
3. **Start the servers**:
   
   **Terminal 1:**
   ```bash
   cd backend && mvn spring-boot:run
   ```
   
   **Terminal 2:**
   ```bash
   cd frontend && npm run dev
   ```

4. **Access the app**: 
   - VS Code will show port forwarding notifications
   - Click the notification or go to the "Ports" tab
   - Open the forwarded URL for port 3000

## ✅ Verification

### Test the Backend API
```bash
curl http://localhost:8080/api/hello
```
Expected response:
```json
{"message":"Hello World"}
```

### Test the Frontend
1. Open browser to `http://localhost:3000`
2. You should see:
   ```
   React + TypeScript + Spring Boot
   Backend says: Hello World
   ```

## 📁 Project Structure

```
react-ts-springboot-starter/
├── backend/                          # Spring Boot application
│   ├── src/
│   │   └── main/
│   │       ├── java/com/example/demo/
│   │       │   ├── DemoApplication.java
│   │       │   └── controller/
│   │       │       └── HelloController.java
│   │       └── resources/
│   │           └── application.properties
│   └── pom.xml
├── frontend/                         # React + TypeScript app
│   ├── src/
│   │   ├── App.tsx                  # Main component
│   │   ├── main.tsx                 # Entry point
│   │   └── vite-env.d.ts
│   ├── index.html
│   ├── package.json
│   ├── tsconfig.json
│   ├── tsconfig.node.json
│   └── vite.config.ts               # Vite config with proxy
├── .devcontainer/
│   └── devcontainer.json            # Codespaces configuration
└── README.md
```

## 🔧 Configuration

### Backend Configuration

**Port**: Default 8080 (configured in `application.properties`)

**CORS**: Enabled for all origins in development (`@CrossOrigin(origins = "*")`)
⚠️ For production, restrict CORS to specific domains.

### Frontend Configuration

**Port**: Default 3000 (configured in `vite.config.ts`)

**API Proxy**: The frontend proxies `/api/*` requests to `http://localhost:8080`
- This avoids CORS issues during development
- In production, you'll need to configure your server or use environment variables

## 🛠️ Development Tips

### Backend Hot Reload
Use Spring Boot DevTools for automatic restart:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```

### Frontend Environment Variables
Create `frontend/.env` for environment-specific config:
```env
VITE_API_URL=http://localhost:8080
```

### Running Tests

**Backend:**
```bash
cd backend
mvn test
```

**Frontend:**
```bash
cd frontend
npm test  # (Add test dependencies as needed)
```

## 🚢 Production Deployment

### Build for Production

**Backend:**
```bash
cd backend
mvn clean package -DskipTests
# JAR file: target/demo-0.0.1-SNAPSHOT.jar
```

**Frontend:**
```bash
cd frontend
npm run build
# Output: dist/ folder
```

### Deployment Options

1. **Separate Deployment**: Deploy backend and frontend separately
   - Backend: Deploy JAR to cloud platform (AWS, Azure, Heroku, etc.)
   - Frontend: Deploy `dist/` to static hosting (Netlify, Vercel, S3, etc.)

2. **Monolithic**: Serve frontend from Spring Boot
   - Copy `frontend/dist/` to `backend/src/main/resources/static/`
   - Spring Boot will serve the frontend at `/`

## 📝 Adding Features

### Add a New Backend Endpoint
Create a new controller in `backend/src/main/java/com/example/demo/controller/`

### Add a New Frontend Page
Create components in `frontend/src/` and update `App.tsx`

### Add Database Support
Add Spring Data JPA dependency and configure database in `application.properties`

## 🤝 Contributing

This is a starter template. Fork it and customize it for your needs!

## 📄 License

MIT License - Feel free to use this template for any project.

## 🆘 Troubleshooting

### Backend won't start
- Check if port 8080 is already in use: `lsof -i :8080`
- Verify Java 17 is installed: `java -version`

### Frontend won't start
- Check if port 3000 is already in use: `lsof -i :3000`
- Delete `node_modules` and run `npm install` again

### Frontend can't connect to backend
- Ensure backend is running on port 8080
- Check the proxy configuration in `vite.config.ts`
- Verify CORS is enabled in `HelloController.java`

### Codespaces issues
- Check the "Ports" tab to see forwarded ports
- Ensure both servers are running in separate terminals
- Try rebuilding the container: Command Palette → "Rebuild Container"

## 📚 Learn More

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [React Documentation](https://react.dev)
- [Vite Documentation](https://vitejs.dev)
- [TypeScript Documentation](https://www.typescriptlang.org)
