# INTA-CS-Seniors-2027
In-Tech Academy's Computer Science Program, Senior Practicum Course SY 26-27
# Class of 2027 Directory
 
A single-page website that shows a card for every senior in the Class of 2027. 
Each card has a photo, the student's name, their senior quote, a song or artist they have on repeat, a show they can't wait to finish, and (if they want) a link to their portfolio.
 
The site is plain HTML, CSS, and JavaScript. There are no frameworks and no build step.
 
## How it works
 
Each student's card information lives in its own JSON file. When the page loads, JavaScript:
 
1. Reads `students/manifest.json` to find out which student files exist
2. Loads every student file listed there
3. Builds one card per student, in the order the manifest lists them
The manifest is needed because a web browser can't look inside a folder and list the files. Someone has to tell it which files to load.
 
```
class-of-2027/
├── README.md
├── index.html                  ← the page: HTML, CSS, and JavaScript
├── images/                     ← (optional, create it) student photos go here
└── students/
    ├── manifest.json           ← list of student files, in display order
    ├── lastname-firstname.json ← one file per student
    └── ...
```
 
## Add yourself to the directory
 
### 1. Create your file
 
Copy any existing file in `students/` and rename it with your first and last name in lowercase, joined by a hyphen:
 
```
students/lastname-firstname.json
```
 
Use only lowercase letters, numbers, and hyphens. Leave out accents and spaces.
 
### 2. Fill in your information
 
```json
{
  "name": "FirstName LastName",
  "quote": "Your senior quote goes here.",
  "onRepeat": "Song Title by Artist",
  "watching": "Name of the Show",
  "portfolio": "https://your-portfolio-link.com",
  "photo": "images/lastname-firstname.jpg",
  "photoAlt": "Student holding a skateboard in front of a mural"
}
```
 
| Key | Required? | What goes here |
|---|---|---|
| `name` | Yes | Your name as you want it shown |
| `quote` | Yes | Your senior quote |
| `onRepeat` | Yes | A song or artist you have on repeat right now |
| `watching` | Yes | A show you can't wait to finish watching |
| `portfolio` | No | The full link to your portfolio, starting with `https://`. Use `""` to leave it off. |
| `photo` | No | Path to your square photo, like `images/lastname-firstname.jpg`. Use `""` to show your initials instead. |
| `photoAlt` | Only to pair with a photo | A short description of what's in your photo (see step 4) |
 
Don't rename or delete any keys. The page looks for these exact names.
 
If your quote has double quotation marks in it, put a backslash before each one: `"She said \"hi\" first."`
 
### 3. Add your photo (optional)
 
Put your photo in the `images/` folder and name it the same way as your JSON file (`lastname-firstname.jpg`). Square photos look best. Other shapes get cropped to a square from the center.
 
Keep the file small: about 800 × 800 pixels is plenty.
 
### 4. Write your alt text
 
Alt text is what a screen reader says out loud for someone who can't see your photo. Describe what's actually in the picture, since you chose it.
 
- **Good:** `"Student holding a skateboard in front of a mural"`
- **Not useful:** `"Photo of Student"`, since your name is already right there on the card
- **Never:** `"image.jpg"` or `"picture"`

### 5. Add yourself to the manifest
 
Open `students/manifest.json` and add your file name to the list. Every line except the last one needs a comma after it.
 
```json
{
  "students": [
    "lastname-firstname.json"
  ]
}
```
 
> **Class workflow:** Check with Ms. Deehl before editing `manifest.json`. If everyone edits it at the same time, changes can overwrite each other. 
 
## Run it on your computer
 
The page loads files with JavaScript's `fetch()`. For security reasons, browsers block `fetch()` when you open an HTML file by double-clicking it, so you need to run a small local web server. Pick one option:
 
**VS Code:** Install the **Live Server** extension, right-click `index.html`, and choose **Open with Live Server**.
 
**Python**:
 
```bash
cd class-of-2027
python3 -m http.server 8000
```
 
Then go to `http://localhost:8000` in your browser. Press `Ctrl + C` in the terminal to stop the server.
 
If you open the file directly, the page will tell you it needs a web server.
 
## When a card doesn't show up
 
If a student file has a problem, the page still loads every other card and shows a box listing the file and what's wrong.
 
| Message | Likely cause | Fix |
|---|---|---|
| `not valid JSON — check commas and quotation marks` | A comma after the last item, a missing comma, or curly quotes (`“ ”`) around a key or value | Every key and value uses straight double quotes `"`. No comma after the last line before `}`. Paste the file into a JSON validator to find the exact line. |
| `missing name, quote` (or other keys) | A required key is empty, misspelled, or deleted | Compare your keys with the table above. Spelling and capital letters must match exactly (`onRepeat`, not `onrepeat`). |
| `file not found (404)` | The name in `manifest.json` doesn't match the real file name | Check spelling, hyphens, and the `.json` ending in both places. |
| `Couldn't load students/manifest.json` | The manifest itself is broken or missing | Check the manifest for comma or quote mistakes. |
 
A card that loads with a broken photo usually means the `photo` path doesn't match the image's real name or folder. File names are case-sensitive on most web servers, so `Panther.JPG` and `panther.jpg` are different files.
 
## Accessibility
 
The site aims to meet [WCAG 2.2](https://www.w3.org/TR/WCAG22/) Level AA:
 
- Text contrast of at least 4.5:1 in both light and dark mode
- A "Skip to student directory" link and visible focus outlines for keyboard users
- Real headings, lists, and quote markup so screen readers can navigate the page
- Loading progress and the final student count announced to screen readers
- Touch targets at least 44 pixels tall
- Animation turned off for anyone who has reduced motion set on their device
- Layout that works from phone to desktop widths

Writing the code this way is only part of accessibility. Test any changes made to the code base with:
 
- **Keyboard only:** Press `Tab` through the whole page. Can you reach and see every link?
- **A screen reader:** VoiceOver on Mac (`Cmd + F5`) or NVDA on Windows
- **An automated checker:** the [WAVE](https://wave.webaim.org/extension/) or [axe DevTools](https://www.deque.com/axe/devtools/) browser extension
Automated checkers catch only some problems. They can't tell whether your alt text actually describes your photo.
 
## Privacy
 
Before this site goes on a public web address, we will follow In-Tech Academy's media consent process and all students involved will be notified prior. Only share what you're comfortable with anyone on the internet seeing. The portfolio link and photo are optional for this reason.
 
## Customizing the design
 
Colors are set once at the top of the `<style>` block in `index.html` as CSS variables (for example `--royal` and `--gold`). Change them there, and the whole page updates. If you change colors, recheck the contrast with a tool like the [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).
