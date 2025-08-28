# 💬 ChatGPT Process Documentation (Level 1 Submission)

This file documents my ChatGPT conversation while completing the **Take-Home UI Challenge (Book Finder App)**.

---

## 📝 Conversation Summary

**Me (Candidate):**
I applied for a Web Developer position and was given a take-home UI challenge.  
The challenge asks me to pick one of the following tasks:  
1. Book Finder (Open Library API)  
2. Weather Now (Open Meteo API)  
3. Recipe Ideas (TheMealDB API)  
4. Earthquake Visualizer (USGS API + Leaflet)  

I want to build the **Book Finder** app using React + Tailwind CSS. Please help me.  

---

**ChatGPT:**  
Great choice 👍 Book Finder is the simplest and cleanest to implement.  

### Plan:
- UI: Search box + button + grid of results  
- API: `https://openlibrary.org/search.json?title={bookTitle}`  
- Show: cover, title, author, first publish year  
- Responsive with Tailwind  

---

**Me:**  
Write the full React + Tailwind code (ready to paste into CodeSandbox).  

---

**ChatGPT:**  
Sure 🚀 Here’s the complete code:  

```tsx
// App.tsx
import React, { useState } from "react";

interface Book {
  title: string;
  author_name?: string[];
  first_publish_year?: number;
  cover_i?: number;
}

export default function App() {
  const [query, setQuery] = useState("");
  const [books, setBooks] = useState<Book[]>([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  const fetchBooks = async () => {
    if (!query.trim()) {
      setError("Please enter a book title.");
      return;
    }

    setError("");
    setLoading(true);
    setBooks([]);

    try {
      const response = await fetch(
        `https://openlibrary.org/search.json?title=${query}`
      );
      const data = await response.json();

      if (data.docs.length === 0) {
        setError("No books found.");
      } else {
        setBooks(data.docs.slice(0, 20));
      }
    } catch {
      setError("Something went wrong. Try again.");
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="min-h-screen bg-gray-100 p-6">
      <h1 className="text-3xl font-bold text-center mb-6 text-indigo-600">
        📚 Book Finder
      </h1>

      <div className="flex justify-center gap-2 mb-6">
        <input
          type="text"
          placeholder="Search by title..."
          value={query}
          onChange={(e) => setQuery(e.target.value)}
          className="border rounded-lg px-4 py-2 w-64 focus:outline-none focus:ring-2 focus:ring-indigo-400"
        />
        <button
          onClick={fetchBooks}
          className="bg-indigo-600 text-white px-4 py-2 rounded-lg hover:bg-indigo-700 transition"
        >
          Search
        </button>
      </div>

      {loading && <p className="text-center text-gray-600">Loading...</p>}
      {error && <p className="text-center text-red-500">{error}</p>}

      <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 mt-6">
        {books.map((book, index) => (
          <div
            key={index}
            className="bg-white shadow-md rounded-lg overflow-hidden hover:shadow-lg transition"
          >
            <img
              src={
                book.cover_i
                  ? `https://covers.openlibrary.org/b/id/${book.cover_i}-M.jpg`
                  : "https://via.placeholder.com/150x220?text=No+Cover"
              }
              alt={book.title}
              className="w-full h-56 object-cover"
            />
            <div className="p-4">
              <h2 className="text-lg font-semibold">{book.title}</h2>
              <p className="text-gray-600 text-sm">
                {book.author_name ? book.author_name.join(", ") : "Unknown Author"}
              </p>
              <p className="text-gray-500 text-sm">
                {book.first_publish_year || "N/A"}
              </p>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}
```

And in `index.css`:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

**Me:**  
I ran it in CodeSandbox, and it’s working. What’s next?  

---

**ChatGPT:**  
Great 🎉 Now let’s finish **Level 3**:  
- Add code comments  
---

# 📚 Book Finder App
## 🔗 Live Demo
[Click here to view the app on CodeSandbox](https://4tr4zz-5173.csb.app/)
A simple web application built with **React + Tailwind CSS** that allows users to search for books using the **Open Library API**.

## 🚀 Features
- Search books by title
- Display book cover, title, author, and first publish year
- Responsive grid layout (mobile-friendly)
- Error handling:
  - Empty search
  - No results found
  - API/network errors
- Loading state while fetching

## 🛠️ Tech Stack
- **React** (with Hooks for state management)
- **Tailwind CSS** (for styling)
- **Open Library API** (book search)

API endpoint example:

- Add `README.md` with project description, features, tech stack, API reference, and instructions  
- Include screenshot + live demo link  

That’s it ✅  

---

## 🎯 Summary for HR/Reviewer
This ChatGPT session demonstrates:  
- Understanding of requirements  
- Planning and breaking down the task  
- Writing clean React + Tailwind code  
- Handling API calls, state, error, and responsiveness  
- Completing documentation (`README.md`)  

---

✅ This file is included in the submission to satisfy **Level 1: Proof of Process**.
final output link
https://4tr4zz-5173.csb.app/