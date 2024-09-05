---
layout: base
title: Student Home 
description: Home Page
hide: true
image: /images/mario_animation.png
---
<!-- Liquid:  statements -->
<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %} 

<!--- HTML for page contains <p> tag named "Mario" and class properties for a "sprite"  -->

<p id="mario" class="sprite"></p>
  
<!--- Embedded Cascading Style Sheet (CSS) rules, 
        define how HTML elements look 
--->
<style>

  /*CSS style rules for the id and class of the sprite...
  */
  .sprite {
    height: {{pixels}}px;
    width: {{pixels}}px;
    background-image: url('{{sprite_file}}');
    background-repeat: no-repeat;
  }

  /*background position of sprite element
  */
  #mario {
    background-position: calc({{animations[0].col}} * {{pixels}} * -1px) calc({{animations[0].row}} * {{pixels}}* -1px);
  }

</style>

<script>
  ////////// convert YML hash to javascript key:value objects /////////

  var mario_metadata = {}; //key, value object
  {% for key in hash %}  
  
  var key = "{{key | first}}"  //key
  var values = {} //values object
  values["row"] = {{key.row}}
  values["col"] = {{key.col}}
  values["frames"] = {{key.frames}}
  mario_metadata[key] = values; //key with values added

  {% endfor %}

  ////////// game object for player /////////

  class Mario {
    constructor(meta_data) {
      this.tID = null;  //capture setInterval() task ID
      this.positionX = 0;  // current position of sprite in X direction
      this.currentSpeed = 0;
      this.marioElement = document.getElementById("mario"); //HTML element of sprite
      this.pixels = {{pixels}}; //pixel offset of images in the sprite, set by liquid constant
      this.interval = 100; //animation time interval
      this.obj = meta_data;
      this.marioElement.style.position = "absolute";
    }

    animate(obj, speed) {
      let frame = 0;
      const row = obj.row * this.pixels;
      this.currentSpeed = speed;

      this.tID = setInterval(() => {
        const col = (frame + obj.col) * this.pixels;
        this.marioElement.style.backgroundPosition = `-${col}px -${row}px`;
        this.marioElement.style.left = `${this.positionX}px`;

        this.positionX += speed;
        frame = (frame + 1) % obj.frames;

        const viewportWidth = window.innerWidth;
        if (this.positionX > viewportWidth - this.pixels) {
          document.documentElement.scrollLeft = this.positionX - viewportWidth + this.pixels;
        }
      }, this.interval);
    }

    startWalking() {
      this.stopAnimate();
      this.animate(this.obj["Walk"], 3);
    }
    startWalkingLeft() {
      this.stopAnimate();
      this.animate(this.obj["WalkL"], -3);
    }

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startRunningLeft() {
      this.stopAnimate();
      this.animate(this.obj["Run1L"], -6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startCheeringL() {
      this.stopAnimate();
      this.animate(this.obj["CheerL"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startFlippingL() {
      this.stopAnimate();
      this.animate(this.obj["FlipL"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

  window.addEventListener("keydown", (event) => {
    if (event.key === "ArrowRight" || event.key==="d") {   //here I changed it to be right arrow key OR D key, same applied for other keys like down and left
      event.preventDefault();
      if (event.repeat) {
        mario.startCheering();
      } else {
        if (mario.currentSpeed === 0) {
          mario.startWalking();
        } else if (mario.currentSpeed === 3) {
          mario.startRunning();
        }  else if (mario.currentSpeed === -3) {
          mario.startWalking();
        } else if (mario.currentSpeed === -6) {
          mario.startWalking();
        }
      }
    } else if (event.key === "s"||event.key==="ArrowDown") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startFlippingL();
      }
    } else if (event.key === "w"||event.key==="ArrowUp") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startFlipping();
      }
    } else if (event.key === "Space" || event.key===" ") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startPuffing();
      }
    } else if (event.key === "ArrowLeft" || event.key==="a") {
      event.preventDefault();
      if (event.repeat) {
        mario.startCheeringL();
      } else {      // what happens in this giant if and else if statment is that based on the current speed of the sprite (like if its stationary, walking in the correct direction, or walking/running in the opposite directoion) it determines whether it will walk or run in the left direction
        if (mario.currentSpeed === 0) {
          mario.startWalkingLeft();
        } else if (mario.currentSpeed === -3) {
          mario.startRunningLeft();
        } else if (mario.currentSpeed === 3) {
          mario.startWalkingLeft();
        } else if (mario.currentSpeed === 6) {
          mario.startWalkingLeft();
        }
      }
    }
  });

  //touch events that enable animations
  window.addEventListener("touchstart", (event) => {
    event.preventDefault(); // prevent default browser action
    if (event.touches[0].clientX > window.innerWidth / 2) {
      // move right
      if (currentSpeed === 0) { // if at rest, go to walking
        mario.startWalking();
      } else if (currentSpeed === 3) { // if walking, go to running
        mario.startRunning();
      }
    } else {
      // move left
      mario.startPuffing();
    }
  });

  //stop animation on window blur
  window.addEventListener("blur", () => {
    mario.stopAnimate();
  });

  //start animation on window focus
  window.addEventListener("focus", () => {
     mario.startFlipping();
  });

  //start animation on page load or page refresh
  document.addEventListener("DOMContentLoaded", () => {
    // adjust sprite size for high pixel density devices
    const scale = window.devicePixelRatio;
    const sprite = document.querySelector(".sprite");
    sprite.style.transform = `scale(${0.4*scale})`;
    sprite.style.zIndex = "2";
    mario.startResting();
  });
</script>





<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
<script>
  $(document).ready(function() {

      setTimeout(function(){
          $('body').addClass('loaded');
          $('h1').css('color','#222222');
      }, 2000);

      });
</script>

<div id="loader-wrapper">
  <div id="loader"></div>
  <div class="loader-section section-left"></div>
  <div class="loader-section section-right"></div>
</div>

<div style="text-align: center;">
    <img style="box-shadow: 0px 0px 100px #015F83; border-radius: 10px;" src="{{site.baseurl}}/images/AboutMe.png" height="430px" width="550px" alt="freeform"/>
</div>

## Background
-------------------------------------

<div style="background: linear-gradient(to bottom, #260b15, black); padding: 20px; border-radius: 10px;">
    <p style="color: white; font-size: 18px; text-align: center;"> 
        My name is Anvay Vahia. I am 14 years old and have been living in San Diego my whole life. My parents are both from India, so this culture is a pretty big part of my life. Outside of school, I really enjoy tennis and the piano. I have been playing the piano since I was 8 or 9 years old. On the other hand, I started tennis only around 2 years ago, but I am really enjoying it. I also participate in this competition called CyberPatriot. This competition is what inspired me to join CSSE. Some of my hobbies include video games, biking, and going go-karting. I also like spending time with friends when I have the time to do so. 
    </p>
</div>


<div class="button-div" style="text-align: center; margin-top: 40px;">
    <button class="cool-button">Login</button>
    <button class="cool-button">Coding Languages Mini Project</button>
    <a href="https://cyberlord09.github.io/AnvayDNHSCompSci//2023/12/04/PartnerPost.html" target="_blank">
        <button class="cool-button">CTF</button>
    </a>
    </div>

<style>
.button-div {
    position: relative;
    padding: 20px;
    border-radius: 12px;
    animation: glowing 2s infinite;
}

@keyframes glowing {
    0% { box-shadow: 0 0 5px #3498db, 0 0 10px #3498db, 0 0 15px #3498db, 0 0 20px #3498db; }
    50% { box-shadow: 0 0 20px #3498db, 0 0 30px #3498db, 0 0 40px #3498db, 0 0 50px #3498db; }
    100% { box-shadow: 0 0 5px #3498db, 0 0 10px #3498db, 0 0 15px #3498db, 0 0 20px #3498db; }
}

.cool-button {
    background: linear-gradient(45deg, #1e3c72, #2a5298) !important; /* Cool blue gradient */
    border: none !important;
    color: white !important;
    padding: 15px 32px !important;
    text-align: center !important;
    text-decoration: none !important;
    display: inline-block !important;
    font-size: 16px !important;
    margin: 10px !important;
    cursor: pointer !important;
    transition: background 0.3s, transform 0.3s, box-shadow 0.3s !important;
    border-radius: 12px !important;
    position: relative !important;
    overflow: hidden !important;
}

.cool-button::before {
    content: "" !important;
    position: absolute !important;
    top: 50% !important;
    left: 50% !important;
    width: 300% !important;
    height: 300% !important;
    background: rgba(255, 255, 255, 0.15) !important;
    transition: all 0.75s !important;
    border-radius: 50% !important;
    transform: translate(-50%, -50%) scale(0.1) !important;
}

.cool-button:hover::before {
    transform: translate(-50%, -50%) scale(1) !important;
}

.cool-button:hover {
    background: linear-gradient(45deg, #2a5298, #1e3c72) !important; /* Hover blue gradient */
    transform: scale(1.1) !important;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2), 0 12px 40px rgba(0, 0, 0, 0.19) !important;
}

.cool-button:active {
    background: linear-gradient(45deg, #1b2a49, #162a4f) !important; /* Active blue gradient */
    transform: scale(0.9) !important;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2), 0 6px 20px rgba(0, 0, 0, 0.19) !important;
}
</style>