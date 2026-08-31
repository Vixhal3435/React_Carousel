# Ex05 Image Carousel
## Date:28-18-26

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
app.jsx
```
import { useEffect, useState } from "react";
import "./App.css";

function App() {
  const images = [
    "https://images.unsplash.com/photo-1500534623283-312aade485b7?w=1000",
    "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=1000",
    "https://images.unsplash.com/photo-1501785888041-af3ef285b470?w=1000",
    "https://images.unsplash.com/photo-1469474968028-56623f02e42e?w=1000",
    "https://images.unsplash.com/photo-1470770841072-f978cf4d019e?w=1000"
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((currentIndex + 1) % images.length);
  };

  const previousImage = () => {
    setCurrentIndex(
      (currentIndex - 1 + images.length) % images.length
    );
  };

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentIndex((currentIndex) =>
        (currentIndex + 1) % images.length
      );
    }, 3000);

    return () => clearInterval(interval);
  }, [images.length]);

  return (
    <div className="page">
      <h1>React Image Carousel</h1>

      <p className="subtitle">
        Explore beautiful places through images
      </p>

      <div className="carousel">
        <img
          src={images[currentIndex]}
          alt={`Slide ${currentIndex + 1}`}
        />

        <button className="prev" onClick={previousImage}>
          ❮
        </button>

        <button className="next" onClick={nextImage}>
          ❯
        </button>
      </div>

      <div className="dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={index === currentIndex ? "dot active" : "dot"}
            onClick={() => setCurrentIndex(index)}
          ></span>
        ))}
      </div>
    </div>
  );
}

export default App;
```
app.css
```
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #fda874;
}

.page {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 55px;
}

h1 {
  margin: 0;
  color: #222;
  font-size: 38px;
  font-weight: 700;
}

.subtitle {
  margin: 10px 0 30px;
  color: #666;
  font-size: 17px;
}

.carousel {
  width: 850px;
  height: 480px;
  position: relative;
  overflow: hidden;
  border-radius: 18px;
  background: white;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.carousel img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 50px;
  height: 50px;
  border: none;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.55);
  color: white;
  font-size: 24px;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  background: rgba(0, 0, 0, 0.8);
  transform: translateY(-50%) scale(1.08);
}

.prev {
  left: 20px;
}

.next {
  right: 20px;
}

.dots {
  display: flex;
  justify-content: center;
  gap: 9px;
  margin-top: 22px;
}

.dot {
  width: 12px;
  height: 12px;
  background: #aaa;
  border-radius: 50%;
  cursor: pointer;
  transition: 0.3s;
}

.dot.active {
  background: #333;
  transform: scale(1.2);
}

@media (max-width: 900px) {
  .carousel {
    width: 90%;
    height: 400px;
  }
}

@media (max-width: 600px) {
  h1 {
    font-size: 28px;
  }

  .carousel {
    height: 300px;
  }
}
```

## OUTPUT
![alt text](image.png)
![alt text](image-1.png)
## RESULT
The program for creating Image Carousel using React is executed successfully.
