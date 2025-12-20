# Local Testing Guide

There are several ways to test this application locally before deploying to Coolify.

## Method 1: Simple HTTP Server (Recommended for Quick Testing)

### Using Python 3
```bash
# Navigate to the project directory
cd /path/to/bitgpa

# Start a local server
python -m http.server 8000

# Or for Python 2
python -m SimpleHTTPServer 8000
```

Then open your browser and visit: `http://localhost:8000`

### Using Node.js (http-server)
```bash
# Install http-server globally (if not already installed)
npm install -g http-server

# Navigate to the project directory
cd /path/to/bitgpa

# Start the server
http-server -p 8000
```

Then visit: `http://localhost:8000`

### Using PHP
```bash
# Navigate to the project directory
cd /path/to/bitgpa

# Start PHP built-in server
php -S localhost:8000
```

### Using Node.js (npx - no installation needed)
```bash
# Navigate to the project directory
cd /path/to/bitgpa

# Start server using npx (no installation needed)
npx http-server -p 8000
```

## Method 2: Test with Docker (Matches Production)

This method tests the exact same setup that will run on Coolify.

### Prerequisites
- Docker installed on your system

### Steps

1. **Build the Docker image:**
   ```bash
   docker build -t bitgpa .
   ```

2. **Run the container:**
   ```bash
   docker run -p 8080:80 bitgpa
   ```
   
   This maps port 8080 on your host to port 80 in the container.

3. **Access the application:**
   Open your browser and visit: `http://localhost:8080`

4. **Stop the container:**
   Press `Ctrl+C` in the terminal, or find the container ID and stop it:
   ```bash
   docker ps
   docker stop <container-id>
   ```

## Method 3: Test Nginx Configuration Locally

If you want to test the exact nginx setup:

1. **Install nginx** on your system

2. **Copy the nginx.conf to nginx sites:**
   ```bash
   # On Linux/Mac
   sudo cp nginx.conf /etc/nginx/sites-available/bitgpa
   sudo ln -s /etc/nginx/sites-available/bitgpa /etc/nginx/sites-enabled/
   ```
   
   Update the `root` path in nginx.conf to point to your project directory:
   ```nginx
   root /absolute/path/to/bitgpa;
   ```

3. **Restart nginx:**
   ```bash
   sudo nginx -t  # Test configuration
   sudo systemctl restart nginx  # Or: sudo service nginx restart
   ```

4. **Access via browser:**
   Visit `http://localhost`

## Quick Test Checklist

When testing locally, verify:

- [ ] Home page loads and displays all semesters/subjects
- [ ] Can select grades for subjects
- [ ] GPA calculation works correctly
- [ ] Navigation between pages (Home, FAQ, About, Contact) works
- [ ] All images and icons load properly
- [ ] Fonts are loading correctly
- [ ] Mobile responsive design works (test on different screen sizes)
- [ ] JSON data loads from `data/subjects.json`

## Troubleshooting

### CORS Errors
If you see CORS errors, make sure you're using an HTTP server (Method 1) and not opening the HTML file directly with `file://` protocol.

### Port Already in Use
If port 8000 is already in use, try a different port:
```bash
python -m http.server 8080
# or
http-server -p 3000
```

### Docker Issues
- Make sure Docker is running
- Check if port 8080 is available (or use a different port: `docker run -p 3000:80 bitgpa`)
- View Docker logs: `docker logs <container-id>`

### Assets Not Loading
- Check browser console for 404 errors
- Verify file paths are correct
- Ensure all files are in the project directory

