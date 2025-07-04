QR Code Generator
A simple Node.js application that generates QR code images from user-provided URLs using the inquirer and qr-image npm packages. This project also demonstrates basic file system operations using the native fs module.
Table of Contents

Prerequisites
Installation
Usage
How It Works
Project Structure
License

Prerequisites

Node.js (v14 or higher recommended)
npm (comes with Node.js)
A terminal or command-line interface

Installation

Clone the repository or download the project files to your local machine:
git clone <your-repo-url>
cd QRCodeProj


Initialize the project:Run the following command to create a package.json file:
npm init

Follow the prompts to set up the project details (e.g., name, version, author). You can use the default settings or customize them as shown in the example:
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


Install dependencies:Install the required npm packages:
npm install inquirer qr-image



Usage

Run the application:
node index.js


Enter a URL when prompted (e.g., https://www.google.com).

The application will:

Generate a QR code image named qr_img.png in the project directory.
(Optional) Save the entered URL to a text file (see How It Works for adding this feature).


Open the generated qr_img.png to scan the QR code, which will direct to the provided URL.


Example terminal interaction:
? Type in your URL: https://www.google.com

This generates a QR code for https://www.google.com.
How It Works
The application is built step-by-step as follows:

User Input with Inquirer:

The inquirer package prompts the user to input a URL via the terminal.
The input is captured and stored for further processing.


QR Code Generation:

The qr-image package converts the user-provided URL into a QR code image.
The generated QR code is saved as qr_img.png in the project directory using the fs module.


Saving User Input (Optional):

To save the user-entered URL to a text file, you can extend the code by adding:fs.writeFileSync('url.txt', url);

This creates a url.txt file containing the URL.



Here’s the complete code for reference:
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
    // Optional: Save URL to a text file
    // fs.writeFileSync('url.txt', url);
  })
  .catch((error) => {
    if (error.isTtyError) {
      console.log("Prompt couldn't be rendered in the current environment");
    } else {
      console.log("Something went wrong:", error);
    }
  });

Project Structure
QRCodeProj/
├── index.js           # Main application file
├── package.json       # Project metadata and dependencies
├── qr_img.png        # Generated QR code image
├── url.txt           # (Optional) File to store user-entered URL

License
This project is licensed under the ISC License. See the package.json for details.
