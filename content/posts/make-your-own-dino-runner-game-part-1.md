+++
date = '2025-06-18T12:47:43+05:30'
draft = false 
title = '🦖 Code Like a Caveman: Make Your Own Dino Runner Game (Part 1)!.'
+++

Ever wanted to build your own game but didn’t know where to start? You’ve come to the right place. In this guide we will share a step by step roadmap for creating your own Dino Runner Game.

Before starting you need to have a basic knowledge of **HTML/CSS & JavaScript**. Apart from them here are the tools that you need:

- **Text Editor** - A basic editor like Notepad will also do, but if you’re feeling like Sensei then you can choose VS Code.
- **Web Browser** - A omni-present browser like [Google Chrome](https://www.google.com/chrome/what-you-make-of-it/) should work fine, but if you want to choose an alternate browser, we recommend [Firefox](https://www.mozilla.org/en-US/firefox/new/?utm_campaign=SET_DEFAULT_BROWSER) or [Brave](https://brave.com/)
- **Github (optional)** - [Github](https://github.com/) can be a good place to host your code for free. You are also free to choose any source control as per your choice.


Ok, enough of the prep talk, if you’ve gathered all these tools then let’s get our hands dirty and move on to the (messy) coding part.

 
## Step 1: Create the Game Layout

In our first step, we will be setting up the skeleton of our game environment - the desert where our brave little dino will endlessly run. We will be using basic HTML for this purpose. 

index.html

```

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dino Game</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div id="game">
    <div id="dino"></div>
    <div id="cactus"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>

```


**Code Explanation:**

- ``` #game ``` - The main game area (our desert)
- ``` #dino ``` - The player character (Our own Dino)
- ``` #cactus ``` - The obstacle (which we need to avoid)


## Step 2: Style the Dino & the Desert

For styling our game we will be going old school and using the CSS to create a basic retro look for the game. 

*style.css*

```

/* Reset default styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #f7f7f7;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: sans-serif;
}

/* Game Area */
#game {
  width: 800px;
  height: 200px;
  background-color: #fff;
  border: 2px solid #444;
  position: relative;
  overflow: hidden;
}

/* Dino */
#dino {
  width: 40px;
  height: 40px;
  background-color: #333;
  position: absolute;
  bottom: 0;
  left: 50px;
  transition: bottom 0.1s;
}

/* Cactus */
#cactus {
  width: 25px;
  height: 50px;
  background-color: green;
  position: absolute;
  bottom: 0;
  right: -30px;
}


```


**Code Explanation:**

- Give you a clean game area (``` #game ```) with a dimension of 800 x 200 pixels
- Gives a basic styling to our dino (Don’t worry if it looks like a **boxy dino**, we will shape it further later in our guide)
- Position everything so the dino starts from the left and the cacti comes in from right.

We will customize the colors, sizes, or even add a sprite image later.



## Step 3: Making the Dino Jump

Now that the basic structure of Dino and cacti is ready, we can focus on building the basic functionality for the game, for which we will be using JavaScript.

*script.js:*

```

const dino = document.getElementById("dino");

let isJumping = false;
let jumpHeight = 0;
let gravity = 1;
let jumpInterval;

// Listen for spacebar press
document.addEventListener("keydown", function (event) {
  if (event.code === "Space" && !isJumping) {
    jump();
  }
});

function jump() {
  isJumping = true;
  let upInterval = setInterval(() => {
    if (jumpHeight >= 100) {
      clearInterval(upInterval);

      // Fall down
      let downInterval = setInterval(() => {
        if (jumpHeight <= 0) {
          clearInterval(downInterval);
          isJumping = false;
        } else {
          jumpHeight -= 5;
          dino.style.bottom = jumpHeight + "px";
        }
      }, 20);
    } else {
      jumpHeight += 5;
      dino.style.bottom = jumpHeight + "px";
    }
  }, 20);
}

```


What This code Does:

- This code will make our runner character (which still looks like square box 😂) jump using ``` jumpHeight ```
- Then makes the runner character / dino land by reversing the direction (``` jumpHeight -= 5; ```)
- Prevents our runner character from double jumping by using the ``` isJumping ``` flag.


## Conclusion: You’ve Just taken the First Leap

Congratulations! 🎉 You’ve officially laid down the foundation for your very own [Dino Runner Game](https://dinogamerunner.in/) — from structuring the HTML layout to styling your dino and even making it jump with JavaScript. 

Sure, our dino still looks a bit *boxy* and the desert is quiet for now, but don’t worry — this is just the beginning of your coding adventure. In the **next part**, we’ll bring the game to life by adding **moving obstacles**, **collision detection**, **game-over logic**, and maybe even some **sound effects** and a **score counter** to spice things up!

So grab a snack, stretch those fingers, and stay tuned — your Dino Game journey is just getting started. 

Want to be the first to know when the next part drops? Bookmark this blog or subscribe to our newsletter for updates!

**Until then, code like a caveman… but debug like a pro.**
