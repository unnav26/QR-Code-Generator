# QR Code Generator

A simple Node.js application that generates QR code images from user-provided URLs using the `inquirer` and `qr-image` npm packages. This project also demonstrates basic file system operations using the native `fs` module.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Project Structure](#project-structure)
- [License](#license)

## Prerequisites
- [Node.js](https://nodejs.org/) (v14 or higher recommended)
- npm (comes with Node.js)
- A terminal or command-line interface

## Installation
1. **Clone the repository** or download the project files:
   ```bash
   git clone <your-repo-url>
   cd QRCodeProj

2. **Initialize the project**:
   ```bash
   npm init
   ```
   Follow prompts; use defaults or set:
   ```json
   {
     "name": "2.4-qr-code-project",
     "version": "1.0.0",
     "type": "module",
     "main": "index.js",
     "author": "Unnav Sharma",
     "license": "ISC",
     "dependencies": {
       "fs": "^0.0.1-security",
       "inquirer": "^9.3.7",
       "qr-image": "^3.2.0"
     }
   }
   ```

3. **Install dependencies**:
   ```bash
   npm install inquirer qr-image
   ```

## Usage
1. Run the app:
   ```bash
   node index.js
   ```

2. Enter a URL (e.g., `https://www.google.com`).

3. Check the generated `qr_img.png` in the directory to scan the QR code.
   - Optional: Add `fs.writeFileSync('url.txt', url);` to save the URL to a text file.

Example:
```bash
? Type in your URL: https://www.google.com
```

## How It Works
- **User Input**: `inquirer` prompts for a URL.
- **QR Generation**: `qr-image` creates a QR code, saved as `qr_img.png` with `fs`.
- **Optional Save**: Add `fs.writeFileSync('url.txt', url);` to store the URL.

Code:
```javascript
import inquirer from "inquirer";
import qr from "qr-image";
import fs from "fs";

inquirer
  .prompt([
    {
      message: "Type in your URL:",
      name: "URL",
    },
  ])
  .then((answers) => {
    const url = answers.URL;
    var qr_svg = qr.image(url);
    qr_svg.pipe(fs.createWriteStream('qr_img.png'));
    // Optional: fs.writeFileSync('url.txt', url);
  })
  .catch((error) => {
    if (error.isTtyError) {
      console.log("Prompt couldn't be rendered in the current environment");
    } else {
      console.log("Something went wrong:", error);
    }
  });
```

## Project Structure
```
QRCodeProj/
├── index.js           # Main application file
├── package.json       # Project metadata and dependencies
├── qr_img.png        # Generated QR code image
├── url.txt           # (Optional) File to store user-entered URL
```

