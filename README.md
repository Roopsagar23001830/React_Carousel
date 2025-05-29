# Ex05 Image Carousel
## Date:29/05/2025

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
# App.js
```
import React, { useState, useEffect } from 'react';

function App() {
  const images = [
    'https://images.unsplash.com/photo-1470252815962-d4550e854972?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D', 
    'https://images.unsplash.com/photo-1469474968028-5672d492f65c?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D', 
    'https://images.unsplash.com/photo-1475924156734-ce853f778297?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D', 
    'https://images.unsplash.com/photo-1447752875215-b2761acb3c5d?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D', 
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex - 1 + images.length) % images.length);
  };

  useEffect(() => {
    const interval = setInterval(nextImage, 3000);
    return () => clearInterval(interval);
  }, [nextImage]);

  return (
    <div className="min-h-screen bg-gradient-to-br from-indigo-50 to-purple-100 flex flex-col items-center justify-center p-4 font-inter">
      <div className="bg-white p-6 rounded-2xl shadow-2xl w-full max-w-3xl transform transition-all duration-300 hover:scale-[1.01]">
        <h1 className="text-4xl font-extrabold text-center text-indigo-800 mb-8 tracking-tight">
          Dynamic Image Showcase
        </h1>

        <div className="relative w-full aspect-video rounded-xl overflow-hidden shadow-lg mb-6">
          <img
            src={images[currentIndex]}
            alt={`Carousel Image ${currentIndex + 1}`}
            className="w-full h-full object-cover transition-opacity duration-700 ease-in-out"
            style={{ opacity: 1 }}
            onError={(e) => { e.target.onerror = null; e.target.src='https://placehold.co/800x450/CCCCCC/333333?text=Image+Error'; }}
          />
          <div className="absolute inset-0 flex items-center justify-between p-4">
            <button
              onClick={prevImage}
              className="bg-black bg-opacity-40 text-white p-3 rounded-full hover:bg-opacity-60 transition duration-300 focus:outline-none focus:ring-2 focus:ring-white focus:ring-opacity-75"
            >
              <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M15 19l-7-7 7-7" />
              </svg>
            </button>
            <button
              onClick={nextImage}
              className="bg-black bg-opacity-40 text-white p-3 rounded-full hover:bg-opacity-60 transition duration-300 focus:outline-none focus:ring-2 focus:ring-white focus:ring-opacity-75"
            >
              <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M9 5l7 7-7 7" />
              </svg>
            </button>
          </div>
        </div>

        <div className="flex justify-center space-x-2 mb-8">
          {images.map((_, index) => (
            <button
              key={index}
              onClick={() => setCurrentIndex(index)}
              className={`h-3 w-3 rounded-full transition-colors duration-300 ${
                index === currentIndex ? 'bg-indigo-600 scale-125' : 'bg-gray-300 hover:bg-gray-400'
              }`}
              aria-label={`Go to image ${index + 1}`}
            ></button>
          ))}
        </div>
      </div>

      <footer className="mt-10 text-center text-gray-600 text-sm">
        <p>&copy; {new Date().getFullYear()} Image Carousel. All rights reserved.</p>
        <p>Developed by: Roop Sagar S L</p>
        <p>Register Number: 212223040175</p>
      </footer>
    </div>
  );
}

export default App;

```
# App.css
```
body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  background: #f5f5f5;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.carousel-container {
  text-align: center;
  padding: 2rem;
  background: white;
  margin-top: 3rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border-radius: 12px;
}

.carousel {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 1rem 0;
}

img {
  width: 600px;
  height: 300px;
  border-radius: 8px;
  object-fit: cover;
}

.nav-button {
  background: rgba(0, 0, 0, 0.6);
  border: none;
  color: white;
  font-size: 2rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
}

.nav-button:first-of-type {
  left: 0;
}

.nav-button:last-of-type {
  right: 0;
}

footer {
  margin-top: 2rem;
  font-size: 1rem;
  color: #555;
}

```

## OUTPUT

![Screenshot 2025-05-29 162524](https://github.com/user-attachments/assets/cb2befa0-e553-4365-8a11-f12ed4247fee)


## RESULT
The program for creating Image Carousel using React is executed successfully.
