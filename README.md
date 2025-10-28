# MWAD_EX05_image-carousel-in-react
## Date: 28/10/2025

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
image_carousel.jsx
```
import React, { useState, useEffect } from "react";

const Carousel = ({ images }) => {
  const [index, setIndex] = useState(0);

  // Next and Previous Buttons
  const nextSlide = () => {
    setIndex((prev) => (prev + 1) % images.length);
  };

  const prevSlide = () => {
    setIndex((prev) => (prev - 1 + images.length) % images.length);
  };

  // Auto-Rotate every 3 seconds
  useEffect(() => {
    const timer = setInterval(nextSlide, 3000);
    return () => clearInterval(timer);
  }, []);

  // Inline styles
  const styles = {
    carousel: {
      position: "relative",
      width: "600px",
      height: "350px",
      margin: "40px auto",
      overflow: "hidden",
      borderRadius: "10px",
      boxShadow: "0 4px 12px rgba(0, 0, 0, 0.3)",
    },
    inner: {
      display: "flex",
      transition: "transform 0.6s ease-in-out",
      transform: `translateX(-${index * 100}%)`,
    },
    img: {
      width: "600px",
      height: "350px",
      objectFit: "cover",
    },
    button: {
      position: "absolute",
      top: "50%",
      transform: "translateY(-50%)",
      backgroundColor: "rgba(0, 0, 0, 0.5)",
      border: "none",
      color: "white",
      fontSize: "24px",
      padding: "10px",
      cursor: "pointer",
      borderRadius: "50%",
    },
    prev: {
      left: "10px",
    },
    next: {
      right: "10px",
    },
  };

  return (
    <div style={styles.carousel}>
      <div style={styles.inner}>
        {images.map((img, i) => (
          <img key={i} src={img} alt={`Slide ${i}`} style={styles.img} />
        ))}
      </div>

      <button onClick={prevSlide} style={{ ...styles.button, ...styles.prev }}>
        ❮
      </button>
      <button onClick={nextSlide} style={{ ...styles.button, ...styles.next }}>
        ❯
      </button>
    </div>
  );
};

export default Carousel;
```

app.jsx
```
import Carousel from "./image_Carousel";

function App() {
  const images = [
    "https://picsum.photos/id/1018/600/350",
    "https://picsum.photos/id/1021/600/350",
    "https://picsum.photos/id/1025/600/350",
    "https://picsum.photos/id/1028/600/350",
  ];

  return (
    <div>
      <h2 style={{ textAlign: "center" }}>Image Carousel</h2>
      <Carousel images={images} />
    </div>
  );
}

export default App;
```


## OUTPUT

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2d30fc7e-25e5-45be-a28d-4f7988a2e5bf" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
