# Technical Documentation: Lemon Cafe Project

This document provides in-depth technical details about the structure, styling, scripts, animation configurations, and customization instructions for the **Lemon Cafe** project.

---

## 📂 1. Directory Tree & Architecture

The project has a flat folder structure representing a single-page marketing landing page with an associated registration form:

```text
LemonCafeProje/
├── css/
│   ├── search.js       # Search input activation script
│   └── style.css       # Main stylesheet containing all custom CSS layouts
├── img/                # Graphic assets (menus, cafe storefront, menu items)
│   ├── Bej ve Siyah Sade Restoran Kafe Menü.jpg
│   ├── LımonCaffeDukkan.jpg
│   ├── LemonCoffeDukkan2.jpg
│   ├── cake.jpg
│   ├── chocalate.jpg
│   ├── cookies.jpg
│   ├── dondurma.jpg
│   ├── kahveÇekirdeği.jpg
│   ├── latte.jpg
│   ├── pasta.jpg
│   └── sıcakÇikolata.jpg
├── .gitattributes      # Git attribute rules
├── Anasayfa.html       # Landing page containing HTML and ScrollReveal animations
└── Form.html           # Bootstrap-styled registration page
```

---

## 📄 2. Page Analysis & Logic

### 🏠 2.1. `Anasayfa.html` (Landing Page)
This is the core page. It is structured into semantic HTML5 sections:
1. **`<header id="header">`**: Features the navbar, site title brand, and page links. It includes a search bar element (`#searchEngine`) controlled by `/css/search.js`.
2. **`Hero Text`**: Centered greeting banner containing the call-to-action button `Giriş` (pointing to `Form.html`).
3. **`Hakkımızda` Section (`#about`)**: Introduces the café. Features side-by-side flexbox configuration (image on the left, copy on the right).
4. **`Bilgi` Section (`#portfolio`)**: A 2D gallery showcasing items. Implements CSS overlays and image scaling on hover.
5. **`Menü` Section (Alternative `#about`)**: Spotlights the cafe's menu image and ingredients list.
6. **`Hizmetlerimiz` Section (`#Hizmetlerimiz`)**: A Bootstrap grid (`col-md-4`) showcasing:
   * Coffees
   * Desserts
   * Appetizers
7. **`İletişim` Section (`#contact`)**: Addresses, telephone numbers, and email info mapped under Bootstrap column layouts.

#### 💫 ScrollReveal Animation Configurations:
The landing page relies on the `ScrollReveal` library to trigger animations when the user scrolls down.
* **Left Reveal (`.anime-left`)**:
  - Origin: Left
  - Distance: `25rem`
  - Duration: `1000ms`
  - Delay: `300ms`
* **Right Reveal (`.anime-right`)**:
  - Origin: Right
  - Distance: `25rem`
  - Duration: `1000ms`
  - Delay: `600ms`
* **Top Reveal (`.anime-top`)**:
  - Origin: Top
  - Distance: `25rem`
  - Duration: `1000ms`
  - Delay: `300ms`
* **Bottom Reveal (`.anime-bottom`)**:
  - Origin: Bottom
  - Distance: `25rem`
  - Duration: `1000ms`
  - Delay: `600ms`
* **Sequential Delays (ani1 to ani8)**:
  - Applied to gallery/portfolio items (`.portfolio-item`) with incremental delays starting from `250ms` up to `2000ms` to produce a staggered fade-in effect.

---

### 📝 2.2. `Form.html` (Registration Form)
A single signup landing page:
- Uses a full-screen blurred background image of the storefront (`LımonCaffeDukkan.jpg`).
- The form container uses an absolute-centered translucent white panel:
  `background-color: rgba(255, 255, 255, 0.8)`
- Uses Bootstrap's form control components.
- Standard form inputs:
  - Ad (First Name) - Text
  - Soyad (Last Name) - Text
  - Email - Email
  - Şifre (Password) - Password
  - Cinsiyet (Gender) - Inline Radio inputs

---

### 🛠️ 2.3. JavaScript Functionality

#### Search Input Toggle (`css/search.js`)
Handles the animated expand/collapse search bar:
```javascript
const searchIcon = document.getElementById('searchIcon')
const searchEngine = document.getElementById('searchEngine')

searchIcon.addEventListener('click', () => {
    searchEngine.classList.toggle('active')
})
```
When class `.active` is added, the search engine input changes its width to `70%` and opacity to `1` over a transition period of `0.5s`.

#### Mobile Navigation Menu (`Anasayfa.html` L289-L299)
Toggles the dropdown navigation menu on small devices by adjusting `maxHeight`:
```javascript
var menuItems = document.getElementById('menuItems');
menuItems.style.maxHeight = "0px";

function menuToggle(){
  if(menuItems.style.maxHeight == "0px"){
    menuItems.style.maxHeight = "200px";
  } else {
    menuItems.style.maxHeight = "0px";
  }
}
```

---

## 🎨 3. CSS System & Styling Details (`css/style.css`)

### Typography
- Font Family: **Poppins** (San-serif) imported from Google Fonts.
- Script Cursive Fonts: **Herr Von Muellerhoff** (applied to main `<h1>` "Hosgeldiniz") and **Playwrite CU** (applied to headings like "Hakkımızda").

### Theme Palette
The theme uses a warm, cozy palette suitable for a coffee shop:
- Primary Warm Orange: `rgb(255, 166, 0)`
- Secondary Dark Brown: `#5b2a02` (used for the portfolio overlay)
- Accent Amber: `rgb(205, 142, 25)` (used for buttons and icons)

### Gallery Hover Effects
The showcase items (`.portfolio-item`) have high-quality zoom-in transitions:
```css
.portfolio-item img {
    transition: .5s;
}
.portfolio-item:hover img {
    transform: scale(1.2);
}
.portfolio-item:hover .overlay {
    top: 0; /* Slides the brown icon overlay upwards */
}
```

---

## 🔧 4. How to Customize and Extend

### How to Add a New Item to the Gallery:
1. Save your image inside the `img/` folder (e.g., `img/new_coffee.jpg`).
2. Add a new `portfolio-item` block to the `#portfolio` container:
   ```html
   <div class="portfolio-item ani8">
     <img src="/img/new_coffee.jpg" />
     <div class="overlay">
       <i class="bi bi-cup-hot-fill"></i>
     </div>
   </div>
   ```
3. Assign a delay class (`ani1` to `ani8`) to align it with ScrollReveal's timeline.

### How to Modify ScrollReveal Delays:
Modify the `<script>` tag at the bottom of `Anasayfa.html` to adjust trigger times. For example, to make the first item load faster:
```javascript
ScrollReveal().reveal('.ani1', { delay: 100 }); // Changed from 250 to 100
```

---

## 🚀 5. Roadmap & Future Recommendations

1. **Backend Form Submission**: Currently, `Form.html` is static. Connecting it to a backend or serverless function (like Firebase or Formspree) will enable actual registration tracking.
2. **Search Logic Integration**: Enable filtering in the gallery list or directing search queries to specific sections of the landing page.
3. **Menu JSON Database**: Instead of rendering a static menu image, fetch a JSON menu database to display items dynamically with pricing and descriptions.
4. **Dark Mode Theme**: Add a dark mode toggle to shift the light background colors to a rich dark cocoa scheme.


<!-- GPG Duzeltme Testi -->
