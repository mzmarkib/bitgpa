# BIT GPA Calculator

A comprehensive, cumulative GPA calculator designed specifically for Bachelors in Information Technology (BIT) students at the University of Colombo School of Computing (UCSC). This Progressive Web App (PWA) helps students calculate their Grade Point Average across all semesters, track their academic progress, and predict their degree classification.

## 🌐 Live Demo

**👉 [Try the app live: https://bitgpa.demo.avalondigital.lk](https://bitgpa.demo.avalondigital.lk)**

## ✨ Features

### Core Functionality
- **Cumulative GPA Calculation**: Calculate GPA across all semesters in one go
- **Multiple Attempt Support**: Handle 1st and 2nd attempts with proper GPA cap rules
- **Grade Selection Interface**: Easy-to-use interface with all UCSC grade options (A+, A, A-, B+, B, B-, C+, C, C-, D+, D, D-, E, NOT SAT)
- **Honors Class Prediction**: Automatically determines expected degree classification
- **Comprehensive FAQ**: Detailed answers to common GPA calculation questions

### Technical Features
- **Progressive Web App (PWA)**: Installable on mobile and desktop devices
- **Offline Support**: Works without internet connection after first visit
- **Auto-Save**: Automatically saves your GPA selections using local storage
- **Auto-Restore**: Loads your previous selections when you return
- **Add to Home Screen**: Smart prompt to install the app
- **SEO Optimized**: Comprehensive meta tags, Open Graph, Twitter Cards, and Schema.org structured data
- **Performance Optimized**: Resource preloading, lazy loading, optimized JavaScript
- **Dynamic Contact Info**: Contact information loaded from JSON file
- **Pure Vanilla JavaScript**: No frameworks or libraries - lightweight and fast

## 📖 How It Works

1. **Load Subjects**: The app loads all BIT subjects from `data/subjects.json`
2. **Select Grades**: Students select grades for subjects they've completed
3. **Set Attempts**: Mark whether each subject is a 1st or 2nd attempt
4. **Calculate GPA**: The app calculates cumulative GPA using the formula:
   ```
   GPA = Σ(GPV × Credits) / Σ(Credits)
   ```
5. **Apply Rules**: Special rules apply for second attempts (capped at 2.00 GPV)
6. **Predict Class**: Expected degree classification is calculated based on final GPA thresholds

## 📊 GPA Calculation Rules

### Degree Classifications
- **First Class**: GPA ≥ 3.50
- **Second Class (Upper Division)**: GPA ≥ 3.25
- **Second Class (Lower Division)**: GPA ≥ 3.00
- **General**: GPA < 3.00

### Second Attempt Rules
When a subject is attempted for the second time, even if you score an A or A+, the maximum GPV that can be used in GPA calculation is 2.00 (equivalent to a C grade). This rule ensures fair calculation according to UCSC regulations.

### Grade Point Values (GPV)
| Grade | GPV | Score Range |
|-------|-----|-------------|
| A+ | 4.00 | 90-100 |
| A | 4.00 | 80-89 |
| A- | 3.75 | 75-79 |
| B+ | 3.25 | 70-74 |
| B | 3.00 | 65-69 |
| B- | 2.75 | 60-64 |
| C+ | 2.25 | 55-59 |
| C | 2.00 | 50-54 |
| C- | 1.75 | 45-49 |
| D+ | 1.25 | 40-44 |
| D | 1.00 | 30-39 |
| D- | 0.75 | 20-29 |
| E | 0.00 | 0-19 |

*Note: For class awarding calculations, A+ is given a GPV of 4.25*

## 🚀 Quick Start

### Using the Live Demo
Simply visit **[https://bitgpa.demo.avalondigital.lk](https://bitgpa.demo.avalondigital.lk)** and start calculating!

### Local Development

Since the app uses `fetch()` to load JSON data, you need to use a local HTTP server (opening the HTML file directly won't work due to CORS restrictions).

**Using Python 3:**
```bash
python -m http.server 8000
```

**Using Node.js (no installation needed):**
```bash
npx http-server -p 8000
```

Then visit `http://localhost:8000` in your browser.

### Test with Docker (Production-like)

To test exactly how it will run on Coolify:

```bash
# Build the Docker image
docker build -t bitgpa .

# Run the container
docker run -p 8080:80 bitgpa
```

Visit `http://localhost:8080`

See [TESTING.md](TESTING.md) for more detailed testing instructions.

## 📁 Project Structure

```
.
├── css/              # Stylesheets (SCSS and compiled CSS)
├── data/             # JSON data files
│   ├── subjects.json # Subject data
│   └── contact.json  # Contact information
├── fonts/            # Custom fonts
├── img/              # Images and icons
├── index.html        # Main HTML file
├── Dockerfile        # Docker configuration for deployment
├── nginx.conf        # Nginx server configuration
├── robots.txt        # SEO: Search engine crawler directives
├── sitemap.xml       # SEO: Site structure for search engines
├── manifest.json     # PWA: Web app manifest
├── sw.js             # PWA: Service worker for offline support
└── README.md         # This file
```

## 💾 Local Storage

The app automatically saves your GPA selections to your browser's local storage:
- **What's Saved**: Subject codes, grades (GPV), and attempt status (1st/2nd)
- **When It Saves**: Automatically when you change a grade or attempt status
- **When It Loads**: Automatically when you open the app
- **Privacy**: All data stays on your device - nothing is sent to servers

## 📱 PWA Installation

### Android (Chrome)
1. Visit the website
2. Wait for the install prompt, OR
3. Tap the menu (⋮) → "Install app" or "Add to Home screen"
4. Confirm installation

### iOS (Safari)
1. Visit the website
2. Tap the Share button (□↑)
3. Scroll down and tap "Add to Home Screen"
4. Tap "Add"

### Desktop (Chrome/Edge)
1. Visit the website
2. Click the install icon in the address bar, OR
3. Wait for the install prompt
4. Click "Install"

See [PWA_GUIDE.md](PWA_GUIDE.md) for detailed PWA documentation.

## 🔧 Performance Optimizations

- ✅ Resource preloading (CSS, fonts, JSON data)
- ✅ Deferred script loading
- ✅ Lazy loading for images
- ✅ Optimized JavaScript (reduced DOM queries, efficient loops)
- ✅ Nginx gzip compression and caching headers
- ✅ Minimal dependencies (pure vanilla JS)
- ✅ Service worker for offline functionality

## 🌐 Deployment on Coolify

This project is configured for deployment on [Coolify](https://coolify.io/), a self-hosted alternative to Heroku/Vercel.

### Prerequisites

- A Coolify instance running
- Git repository with this code

### Deployment Steps

1. **Push your code to a Git repository** (GitHub, GitLab, etc.)

2. **In Coolify:**
   - Create a new application
   - Connect your Git repository
   - Coolify will automatically detect the Dockerfile
   - Configure environment variables if needed (none required for this app)
   - Deploy

3. **Coolify will:**
   - Build the Docker image using the Dockerfile
   - Deploy the container with nginx
   - Provide you with a URL for your application

### Manual Docker Build (Optional)

If you want to test the Docker build locally:

```bash
# Build the image
docker build -t bitgpa .

# Run the container
docker run -p 8080:80 bitgpa

# Visit http://localhost:8080
```

## 🛠️ Technologies Used

- **HTML5** (Semantic HTML)
- **CSS3** (SCSS)
- **Vanilla JavaScript** (ES6+)
- **Nginx** (for production deployment)
- **JSON** for data management
- **Service Workers** for PWA functionality

## 📝 FAQ

### How many times can I repeat a subject?
You can have up to Three (3) attempts on a particular subject.

### What is the highest grade for a second attempt?
You can obtain any grade up to an A, but when accounting the Grade Point Value (GPV) for that particular subject in GPA calculation, it can be up to 2.00 (GPV of a C grade) maximum.

### What's the difference between A and A+?
Both A and A+ grades carry the same Grade Point Value (GPV) of 4.00 for regular GPA calculation, but when calculating GPA for class awarding, an A+ will be given a Grade Point Value (GPV) of 4.25.

### What if I miss an exam?
If you are absent for an exam, it will be counted as NOT SAT (not sat). You are expected to produce a medical certificate for your absence.

### What is a Credit?
A credit is the measure of how much content a particular subject carries. A credit is equal to 15 hours of lectures or 30-45 hours of practical or an equivalent combination of lectures.

## 📧 Contact

- **Name**: M. Z. Mohammed Arkib
- **Handle**: @mzmarkib
- **Email**: [hi@mzmarkib.site](mailto:hi@mzmarkib.site)
- **Social Media**: Find me on Twitter, GitHub, LinkedIn using the handle @mzmarkib

## 📄 License

This project is open source and available for educational purposes.

## 🤝 Contributing

Feel free to submit issues or pull requests if you find bugs or want to add features. This app was built for practice and to help BIT students, so any improvements are welcome!

## 🙏 Acknowledgments

- Built for BIT students at University of Colombo School of Computing (UCSC)
- Created as a practice project to help students calculate their GPA easily
- No frameworks or libraries were used - pure HTML, CSS, and JavaScript

---

**Made with ❤️ for BIT Students | [Live Demo](https://bitgpa.demo.avalondigital.lk)**
