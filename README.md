# AngElectron

$ npm i -g @angular/cli

$ ng new ang-electron

$ cd ang-electron

$ npm i -D electron@latest


create main.js file in root directory and put the content below


<------------------------ Start main.js ------------------------------>



const { app, BrowserWindow } = require("electron");

const path = require("path");

const url = require("url");

let win;

function createWindow() {

  win = new BrowserWindow({ width: 800, height: 600 });
  

  // load the dist folder from Angular
  
  win.loadURL(
  
    url.format({
    
      pathname: path.join(__dirname, `/dist/index.html`),
      
      protocol: "file:",
      
      slashes: true
      
    })
    
  );
  

  // The following is optional and will open the DevTools:
  
  // win.webContents.openDevTools()
  

  win.on("closed", () => {
  
    win = null;
    
  });
  
}


app.on("ready", createWindow);


// on macOS, closing the window doesn't quit the app

app.on("window-all-closed", () => {

  if (process.platform !== "darwin") {
  
    app.quit();
    
  }
  
});


// initialize the app's main window

app.on("activate", () => {

  if (win === null) {
  
    createWindow();
    
  }
  
});




<--------------------------- End main.js ----------------------->




Edit package.json and add below content to script section


"electron-tsc": "tsc main.ts && ng build --base-href ./ && electron ."

"electron": "ng build --base-href ./ && electron .",



Add Below line in package.json 


"main": "main.js", 


Run the app


npm run electron


Create Exe File 


electron-packager <source-dir> <app-name> --platform=win32 --archx64
