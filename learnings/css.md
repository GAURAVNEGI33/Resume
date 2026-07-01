# What I Learned in CSS Day 4

- CSS is used to style HTML pages.
- CSS can be added inline, internal, or external.
- External CSS is best for maintainability.
- Selectors help target HTML elements.
- The DOM can be inspected using Developer Tools.
- CSS should usually be linked in the head tag.
- External CSS is better than inline CSS.
- Classes can be reused.
- IDs should be unique.
- Hover changes the style when the mouse is over an element.
- CSS is linked using:
  <link rel="stylesheet" href="style.css">

 # Day 5 — CSS Learnings

## What I learned today

### 1. Margin & Padding
Today I understood the core box model concepts properly:
- **Margin** — space outside an element, between it and other elements.
- **Padding** — space inside an element, between its content and its border.
- Used both to fix spacing issues in my resume — like the gap between sections, and around my profile photo.

### 2. Centering an Image
I learned how to center an image properly using CSS instead of it being randomly aligned. Used `text-align: center` on the parent `<figure>` tag, and set the image as a block element with `margin: 0 auto` to center it within its container.

### 3. Applying CSS to My Resume
Took my existing resume HTML and added real styling to it — spacing, layout structure (sidebar + main content), borders, and hover effects. This made the resume look much more professional compared to plain unstyled HTML.

### 4. Enhancv (Reference Website)
We discussed Enhancv, a resume-building website, as a reference for what good resume layouts and design choices look like — clean sections, good spacing, clear hierarchy. Useful to compare against while styling my own resume.

### 5. Google Fonts
Learned how to add custom fonts using Google Fonts instead of relying on default system fonts.

**Steps to add a Google Font:**
1. Go to [fonts.google.com](https://fonts.google.com) and pick a font.
2. Copy the `<link>` tag provided.
3. Paste it inside the `<head>` of the HTML file:
   ```html
   <link href="https://fonts.googleapis.com/css2?family=FontName&display=swap" rel="stylesheet">
   ```
4. Apply it in CSS using `font-family`:
   ```css
   body {
     font-family: 'FontName', sans-serif;
   }
   ```

### 6. Image Size & Page Load Speed
Discussed how large image files slow down webpage loading time. A bigger profile photo file size = slower load, especially on slower internet connections.

**Fix — used WebP format:**
- WebP compresses images much better than JPG/PNG while keeping good quality.
- Reduced my profile photo's file size using WebP, which improved load time.
- Also used `width` and `height` attributes on the `<img>` tag so the browser reserves space for the image before it fully loads (avoids layout shift).

## Summary
Today was mainly about applying real CSS to my resume project — spacing with margin/padding, centering elements properly, using custom fonts via Google Fonts, and optimizing image size with WebP for better performance.

# DAY 6 — Resume Project

## 1. Reset
```css
* { margin:0; padding:0; box-sizing:border-box; }
```
Har browser default margin/padding alag deta hai, isliye sabse pehle sab 0 kar diya. `box-sizing: border-box` isliye use kiya taaki padding aur border add hone se element ka width extra na badh jaye — width fix rahega jo maine diya hai.

## 2. Body
```css
body { font-family:"Inter",sans-serif; line-height:1.5; }
```
Font ke baad ek fallback (`sans-serif`) diya hai, agar Inter load na ho toh normal font aa jaye. `line-height:1.5` text ko thoda spaced rakhta hai, padhne mein easy lagta hai.

## 3. Page Layout (Grid)
```css
.page-wrapper { display:grid; grid-template-columns:320px 1fr; margin:0 auto; }
```
Poore page ko Grid se 2 columns mein banaya — left sidebar fix 320px ka, baaki jitni bhi space bache wo right side content le lega (`1fr` matlab remaining space). `margin:0 auto` se pura block center mein aa jata hai.

## 4. Sidebar
Dark background diya, text white — aur white color parent se child elements mein automatically chala jaata hai (inherit hota hai), isliye baar baar likhna nahi pada.

**Profile photo circle:**
```css
.logo { border-radius:50%; }
.logo img { object-fit:cover; }
```
Equal width-height + `border-radius:50%` se image gol ban jaati hai. `object-fit:cover` isliye taaki image stretch na ho, sahi crop ho ke circle fill kare.

**Custom bullets:**
```css
.sidebar ul li::before { content:"◆"; }
```
Default bullet hata ke apna khud ka gold diamond symbol laga diya `::before` se — bina koi extra HTML tag likhe.

**Specific section target karna:**
```css
.sidebar section:nth-of-type(3) dt { }
```
3rd section (Languages wala) ko alag style dena tha, toh class add karne ki jagah `nth-of-type(3)` use kar liya — direct HTML structure se target kar liya.

## 5. Main Content
```css
.content > section > h2::after { content:""; flex:1; background:#C8A24A; }
```
Har heading ke baad ek gold line dikhti hai jo end tak jaati hai — ye ek khali `::after` element hai jise `flex:1` de diya taaki wo baaki space fill kar le.

`>` symbol (child combinator) use kiya taaki sirf direct child section select ho, andar ke nested elements pe effect na pade.

## 6. Job/Project Entries (Grid alignment)
```css
.job { display:grid; grid-template-columns:1fr auto; }
.job h3 { grid-column:1; }
.job .date { grid-column:2; text-align:right; }
.job .employer { grid-column:1/-1; }
```
Job title left, date right — same line pe. Employer wali line ko `1/-1` diya matlab wo pura width le legi (last column tak span karegi).

## 7. Responsive (Media Query)
```css
@media (max-width:850px) {
  .page-wrapper { grid-template-columns:1fr; }
}
```
Chote screen (mobile/tablet) pe 2 columns wala layout single column mein badal jaata hai — sidebar aur content ek ke niche ek aa jaate hain.

---

## Quick Revision (interview ke liye important points)
- `box-sizing:border-box` → width fix rehta hai, padding/border se badhta nahi
- Grid vs Flexbox → Grid 2D (rows+columns) ke liye, Flexbox 1D (ek line align karne) ke liye
- `::before`/`::after` → bina extra HTML ke content add karna
- `>` (child combinator) → sirf direct child select karta hai, sab andar wale nahi
- `nth-of-type()` → class diye bina position se element target karna
- `object-fit:cover` → image ko crop karke fit karta hai, stretch nahi hone deta
- Media query → screen size ke hisaab se CSS badalna (responsive design)

**Common sawal jo pucha ja sakta hai:** "Grid kyu use kiya, Flexbox kyu nahi?" — Answer: pura page layout 2 dimensions (columns + rows) mein set karna tha, isliye Grid better fit tha. Chote alignments (jaise bullet list) ke liye Flexbox use kiya.