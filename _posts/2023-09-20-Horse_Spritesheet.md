---
comments: False
layout: post
title: Animated Horse
description: Spritesheet
type: hacks
courses: {'csse': {'week': 5}}
categories: ['C4.1']
---
<body>
    <div>
        <div id="controls"> <!--basic radio buttons which can be used to check whether each individual animaiton works -->
            <input type="radio" name="animation" id="idle" checked>
            <label for="idle">Start</label><br>
            <input type="radio" name="animation" id="barking">
            <label for="barking">Stop</label><br>        
            <canvas id="spriteContainer"> <!-- Within the base div is a canvas. An HTML canvas is used only for graphics. It allows the user to access some basic functions related to the image created on the canvas (including animation) -->
            <img id="horseSprite" src="{{site.baseurl}}/images/horse.png">
        </canvas>

        </div>
    </div>
</body>
<script>
    window.addEventListener('load', function () {
        const canvas = document.getElementById('spriteContainer');
        const ctx = canvas.getContext('2d');
        const SPRITE_WIDTH = 112;
        const SPRITE_HEIGHT = 84;
        const SCALE_FACTOR = 10;
        const FRAME_LIMIT = 6;
        const FRAME_RATE = 30;
        canvas.width = SPRITE_WIDTH * SCALE_FACTOR;
        canvas.height = SPRITE_HEIGHT * SCALE_FACTOR;
        class Dog {
            constructor() {
                this.image = document.getElementById("horseSprite");
                this.spriteWidth = SPRITE_WIDTH;
                this.spriteHeight = SPRITE_HEIGHT;
                this.width = this.spriteWidth;
                this.height = this.spriteHeight;
                this.x = 0;
                this.y = 0;
                this.scale = 6;
                this.minFrame = 0;
                this.maxFrame = FRAME_LIMIT;
                this.frameX = 0;
                this.frameY = 0;
            }
            draw(context) {
                context.drawImage(
                    this.image,
                    this.frameX * this.spriteWidth,
                    this.frameY * this.spriteHeight,
                    this.spriteWidth,
                    this.spriteHeight,
                    this.x,
                    this.y,
                    this.width * this.scale,
                    this.height * this.scale
                );
            }
            update() {
                if (this.frameX < this.maxFrame) {
                    this.frameX++;
                } else {
                    this.frameX = 0;
                }
            }
        }
        const dog = new Dog();
        // Add event listener to the parent container for event delegation
        const controls = document.getElementById('controls');
        controls.addEventListener('click', function (event) {
            if (event.target.tagName === 'INPUT') {
                const selectedAnimation = event.target.id;
                switch (selectedAnimation) {
                    case 'idle':
                        dog.frameY = 0;
                        break;
                    case 'barking':
                        dog.frameY = 1;
                        break;
                    case 'walking':
                        dog.frameY = 2;
                        break;
                    default:
                        break;
                }
            }
        });
        function animate() {
    setTimeout(function () {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        dog.draw(ctx);
        dog.update();
        requestAnimationFrame(animate);
    }, 1000 / FRAME_RATE); // Calculate the delay based on desired frame rate
}
        animate();
    });
</script>