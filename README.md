# FastAPI URL Shortener

A full-stack URL shortener application built with FastAPI (backend) and React (frontend). This application allows users to shorten long URLs, manage them, and track all shortened links.

![FastAPI URL Shortener](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)

## Features

✨ **Shorten URLs** - Convert long URLs into short, manageable links  
📋 **View All URLs** - Display all shortened URLs in a clean table  
📋 **Copy to Clipboard** - One-click copy functionality for shortened URLs  
🗑️ **Delete URLs** - Remove unwanted shortened URLs  
🔗 **Redirect** - Automatically redirect short URLs to their original destinations  
🎨 **Clean UI** - Modern, responsive interface with intuitive design  

## Tech Stack

### Backend
- **FastAPI** - Modern, fast web framework for building APIs
- **SQLAlchemy** - SQL toolkit and ORM
- **SQLite** - Lightweight database
- **Pydantic** - Data validation using Python type annotations
- **Uvicorn** - ASGI server

### Frontend
- **React** - JavaScript library for building user interfaces
- **Lucide React** - Beautiful icon library
- **Inline Styles** - CSS-in-JS styling approach (no additional CSS frameworks)
- **Fetch API** - For making HTTP requests

## Project Structure

```
.
├── backend/
│   ├── main.py              # FastAPI application
│   ├── urls.db              # SQLite database (auto-generated)
│   └── requirements.txt     # Python dependencies
│
└── frontend/
    ├── public/
    ├── src/
    │   ├── App.js           # Main React component
    │   ├── index.js         # React entry point
    │   └── index.css        # Global styles
    ├── package.json         # Node dependencies
    └── README.md
```

## Installation



### Backend Setup


1. **Create a virtual environment**
   ```bash
   python -m venv venv
   ```

2. **Activate the virtual environment**
   - Windows:
     ```bash
     venv\Scripts\activate
     ```
   - macOS/Linux:
     ```bash
     source venv/bin/activate
     ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the FastAPI server**
   ```bash
   uvicorn main:app --reload
   ```

   The backend will start at `http://localhost:8000`

### Frontend Setup

1. **Navigate to the frontend directory**
   ```bash
   npx create-react-app frontend
   cd frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Install Lucide React icons**
   ```bash
   npm install lucide-react
   ```

4. **Replace the App.js file**
   - Copy the provided React component code into `src/App.js`
   - The component uses inline styles, so no additional CSS setup is needed

5. **Start the React development server**
   ```bash
   npm start
   ```

   The frontend will open at `http://localhost:3000`

## API Documentation

Once the backend is running, visit `http://localhost:8000/docs` for interactive API documentation (Swagger UI).

### Endpoints

#### POST `/shorten`
Create a shortened URL
```json
Request:
{
  "original_url": "https://www.example.com/very/long/url"
}

Response:
{
  "original_url": "https://www.example.com/very/long/url",
  "short_code": "aBc123",
  "short_url": "http://localhost:8000/aBc123"
}
```

#### GET `/all`
Retrieve all shortened URLs
```json
Response:
[
  {
    "original_url": "https://www.example.com/very/long/url",
    "short_code": "aBc123",
    "short_url": "http://localhost:8000/aBc123"
  }
]
```

#### GET `/{short_code}`
Redirect to the original URL
- Returns: HTTP 302 redirect to the original URL
- Error: HTTP 404 if short code not found

#### DELETE `/delete/{short_code}`
Delete a shortened URL
```json
Response:
{
  "detail": "URL deleted successfully"
}
```

## Usage

1. **Open the application** at `http://localhost:3000`
2. **Enter a long URL** in the input field
3. **Click "Shorten"** or press Enter
4. **View your shortened URL** in the table below
5. **Copy the short URL** by clicking the copy icon
6. **Delete URLs** using the trash icon
7. **Visit the short URL** to be redirected to the original

## Configuration

### Change Backend Port
In `backend/main.py`, modify the Uvicorn command:
```bash
uvicorn main:app --reload --port 8080
```

### Change Frontend API URL
In `frontend/src/App.js`, update the API_BASE constant:
```javascript
const API_BASE = 'http://localhost:8080';
```

## Database

The application uses SQLite for data persistence. The database file (`urls.db`) is automatically created when you first run the backend.

### Database Schema

**Table: `urls`**
- `id` (Integer, Primary Key)
- `original_url` (String, Unique, Not Null)
- `short_code` (String, Unique, Indexed, Not Null)

## Features in Detail

### Styling Approach
- Uses inline styles for all styling (no external CSS frameworks required)
- Includes hover effects and interactive states
- Fully responsive design
- No build configuration needed for styles

### URL Shortening Algorithm
- Generates a random 6-character code using letters (a-z, A-Z) and digits (0-9)
- Ensures uniqueness by checking against existing codes
- Total possible combinations: 62^6 = ~56.8 billion URLs

### CORS Configuration
The backend allows all origins for development. For production, update the `allow_origins` in `main.py`:
```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://yourdomain.com"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

## Styling Notes

This project uses **inline styles** instead of CSS frameworks like Tailwind or Bootstrap. This approach:
- ✅ Requires no additional build configuration
- ✅ Works immediately after installation
- ✅ Keeps all styles contained within the component
- ✅ Includes hover effects and interactive states
- ✅ Easy to customize - just modify the `styles` object in `App.js`

If you prefer using Tailwind CSS in the future, you can install it separately and convert the inline styles to Tailwind classes.

## Troubleshooting

### Backend Issues

**Problem:** Module not found error  
**Solution:** Make sure you're in the correct directory and virtual environment is activated

**Problem:** Database locked error  
**Solution:** Close any other applications accessing the database

### Frontend Issues

**Problem:** CORS error  
**Solution:** Ensure the backend is running and CORS is properly configured

**Problem:** Cannot connect to backend  
**Solution:** Verify the backend is running on port 8000 and API_BASE URL is correct

## Future Enhancements

- [ ] Custom short codes (user-defined aliases)
- [ ] Analytics (click tracking)
- [ ] QR code generation
- [ ] Expiration dates for URLs
- [ ] User authentication
- [ ] URL validation and preview
- [ ] Bulk URL shortening
- [ ] Export data (CSV/JSON)

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Author

Created with ❤️ by [Your Name]

## Acknowledgments

- FastAPI documentation
- React documentation
- Lucide React for beautiful icons
- SQLAlchemy for excellent ORM support

---

**Happy URL Shortening! 🚀**


##  --------------push code to github ------------

1. Initialize Git repository
bash
git init
2. Add all files
bash
git add .
3. Create your first commit
bash
git commit -m "Initial commit: FastAPI URL Shortener with React frontend"
4. Create a new repository on GitHub

Go to https://github.com/new
Enter repository name: fastapi-url-shortener (or your preferred name)
Choose Public or Private
DON'T initialize with README (you already have one)
Click "Create repository"

5. Link your local repo to GitHub
Replace YOUR_USERNAME with your GitHub username:
bash
git remote add origin https://github.com/YOUR_USERNAME/fastapi-url-shortener.git
6. Push to GitHub
bash
git branch -M main
git push -u origin main



##  --------------push code to github ------------

1. Initialize Git repository
```bash
git init
```
2. Add all files
```bash
git add .
```
3. Create your first commit
```bash
git commit -m "Initial commit: FastAPI URL Shortener with React frontend"
```
4. Create a new repository on GitHub

Go to https://github.com/new
Enter repository name: fastapi-url-shortener (or your preferred name)
Choose Public or Private
DON'T initialize with README (you already have one)
Click "Create repository"

5. Link your local repo to GitHub
Replace YOUR_USERNAME with your GitHub username:
```bash
git remote add origin https://github.com/YOUR_USERNAME/fastapi-url-shortener.git
```
6. Push to GitHub
```bash
git branch -M main
git push -u origin main
```


# deploy fastapi backend on render.com and render will give a link here you can see your backend 
to make fully working replace the render provided url in frontend source/app.js code 
where we written see the below

replace this to below line.      const API_BASE = 'http://localhost:8000'; // for local development
                                 const API_BASE = 'https://codesera-url-shortener.onrender.com';   // for production or deployed backend (deply on render, paste the render provided link here)

and in backend whereever you mention localhost replace with this link 
"https://codesera-url-shortener.onrender.com" 
on github and again deploy this on render


# to deploy frontend first make a build file in frontend 
cd frontend 
go to public folder and make a netlify.toml file in this write the below code
```bash
[[redirects]]
from="/*"
to="/index.html"
status=200
```

and then run
```bash
npm run build
```
by npm run build command it will make  a build file 
now go to netlify.com and select manual deploy and drag and drp this build file here
it will deploy and give the link
you can also change the link name , go to project configuration and change the nme
