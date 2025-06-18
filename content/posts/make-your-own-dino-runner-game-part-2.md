+++
date = '2025-06-18T16:09:35+05:30'
draft = false
title = '🦖 Code Like a Caveman: Make Your Own Dino Runner Game (Part 2)!'
+++

Thanks for sticking with us for Part 2 of our series *Code Like a Caveman: Make Your Own Dino Runner Game*. If you haven’t read the first part of the series, you can check it out [here](https://blog.dinogamerunner.in/posts/make-your-own-dino-runner-game-part-1/)

In our first part, we’ve already built the foundation of our Dino Runner Game – the layout (where our runner character still kooks like a box 🫠) using HTML, styling using CSS and the logic with JavaScript (OfCourse).

So, without wasting further time, let’s delve into the next steps of building our own Dino Runner Game.

## Step 4: Moving the Cactus

The cacti needs to be slid in from the right and reset after it passes the dino, thus giving the feel of an endless runner.

Here is the updated  ``` script.js ``` with the cacti logic:

```
const cactus = document.getElementById("cactus");

function startCactusMovement() {
  let cactusPosition = 800; // Start off-screen

  setInterval(() => {
    if (cactusPosition < -25) {
      cactusPosition = 800; // Reset cactus to right
    } else {
      cactusPosition -= 5; // Move left
      cactus.style.right = cactusPosition + "px";
    }
  }, 20);
}

startCactusMovement();

```

**What this code does:**

- Introduces a green colored cacti (which looks like a box for now)
- Starts the cacti at the right edge corner of the screen
- Once it passes through our runner character i.e. dino on the left, it resets back to the right thus creating an illusion of the cacti continuously approaching the dino.

## Step 5: Collision Detection & Game Over functionality

This is the step where our “Dino meets Doom”. We’’ check if the dino and the cacti collide. If it happens, we’ll stop the game and display a Game Over message.

Updated ``` startCactusMovement()  ``` function with collision detection functionality:

```

function startCactusMovement() {
  let cactusPosition = 800;

  const gameLoop = setInterval(() => {
    if (cactusPosition < -25) {
      cactusPosition = 800;
    } else {
      cactusPosition -= 5;
      cactus.style.right = cactusPosition + "px";
    }

    // Get positions for collision detection
    const dinoBottom = parseInt(window.getComputedStyle(dino).getPropertyValue("bottom"));
    const cactusRight = cactusPosition;
    const dinoLeft = 50; // Fixed position of dino

    // Check for collision
    if (
      cactusRight < dinoLeft + 40 &&
      cactusRight > dinoLeft &&
      dinoBottom < 50
    ) {
      alert("💀 Game Over! Press OK to try again.");
      clearInterval(gameLoop);
      window.location.reload(); // Reload the game
    }
  }, 20);
}


```


**Code Explanation:**

- The position of [cacti](https://en.wikipedia.org/wiki/Cacti) is checked against the dino’s location.
- If the cacti overlaps horizontally with the dino and the dino is not jumping and still on the ground, it’s considered a hit.
- Game stops and display a alert with the message : “ 💀 Game Over! Press OK to try again. “, then reloads the page to restart the game so the user can play it again.


## Step 6: Polish the Look & Add Sound

Let’s take our code from the “**Caveman Code**” version to the “**Prehistoric Perfection**” Era. 


Smooth the Jump:

Add a animation which smoothens the animation instead of the old “snapping” jumps:

```

#dino {
  transition: bottom 0.05s linear;
}

```

Add a Ground Line:

```

#ground {
  position: absolute;
  width: 100%;
  height: 5px;
  background-color: #222;
  bottom: 0;
}

```

Then add this to your HTML:

```

<div id="game">
  <div id="ground"></div>
  <div id="dino"></div>
  <div id="cactus"></div>
</div>

```

Pixel Art Sprites

You can replace the coloured boxes with actual Dino and cacti pixel images:

```

#dino {
  background: url('dino-idle.png') no-repeat center/cover;
}

#cactus {
  background: url('cactus-1.png') no-repeat center/cover;
}


```

Just make sure to resize the divs to match the image dimensions.


Add the Gameover and jump sound 

Add these HTML elements inside your <body> tag for adding gameover and jump sound:



```

<audio id="jumpSound" src="assets/jump.wav" preload="auto"></audio>
<audio id="gameOverSound" src="assets/gameover.wav" preload="auto"></audio>

```

Add the following JavaScript logic with these lines:

```

const jumpSound = document.getElementById('jumpSound');

function jump() {
  if (dino.classList != 'jump') {
    dino.classList.add('jump');
    jumpSound.play(); // 🔊 play jump sound
    setTimeout(() => {
      dino.classList.remove('jump');
    }, 300);
  }
}


```

## Conclusion: Dino Game Level-Up! 🦖

Congrats! You’ve just leveled up your [Chrome Dino Game Runner](https://dinogamerunner.in/) from basic blocks to a fun, polished runner — complete with jumping animations, collision detection, pixel sprites, and sound effects.

With every step, you’ve brought the game to life. 🎮
Now you’ve got a solid foundation — and tons of ways to improve it even more: add a score counter, introduce power-ups, or build a custom restart screen.

If you missed **Part 1**, catch up [here](https://blog.dinogamerunner.in/posts/make-your-own-dino-runner-game-part-1/), and stay tuned for **Part 3**, where we take things up another notch!

Until then — keep coding, keep running! 🦕

Note: You can download all the required assets from the file here or get the full source code from [here](https://github.com/pamnanaimanish169/Chrome-Dino-Game-Blog-Tutorial)
