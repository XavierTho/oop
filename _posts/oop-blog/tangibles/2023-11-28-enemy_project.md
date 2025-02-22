---
toc: false
comments: false
layout: post
title: Enemy Project
type: tangibles
courses: { OOP: {week: 0} }
---

<style>
    #canvas {
        margin: 0;
        border: 1px solid white;
    }
</style>
<canvas id='canvas'></canvas>
<script>
    let canvas = document.getElementById('canvas');
    let c = canvas.getContext('2d');
    canvas.width = 650;
    canvas.height = 400;
    let gravity = 1.5;
    class Player {
        constructor() {
            this.position = {
                x: 100,
                y: 200
            };
            this.velocity = {
                x: 0,
                y: 0
            };
            this.width = 30;
            this.height = 30;
        }
        draw() {
            c.fillStyle = 'red';
            c.fillRect(this.position.x, this.position.y, this.width, this.height);
        }
        update() {
            this.draw();
            this.position.y += this.velocity.y;
            this.position.x += this.velocity.x;
            if (this.position.y + this.height + this.velocity.y <= canvas.height)
                this.velocity.y += gravity;
            else
                this.velocity.y = 0;
        }
    }
    class Platform {
        constructor(image) {
            this.position = {
                x: 0,
                y: 300
            }
            this.image = image;
            this.width = 650;
            this.height = 100;
        }
        draw() {
            c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
        }
    }
    class Tube {
        constructor(image) {
            this.position = {
                x: 500,
                y: 180
            }
            this.image = image;
            this.width = 100;
            this.height = 120;
        }
        draw() {
            c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
        }
    }
    class BlockObject {
        constructor(image) {
            this.position = {
                x: 200,
                y: 100
            };
            this.image = image;
            this.width = 158;
            this.height = 79;
        }
        draw() {
            c.drawImage(this.image, this.position.x, this.position.y);
        }
    }
    //--
    // NEW CODE - CREATE GOOMBA CLASS
    //--
    class Goomba {
        constructor(image) {
            this.position = {
                x: 250,
                y: 245
            };
            this.image = image;
            this.width = 55;
            this.height = 55;
            this.visible = true;
            this.velocity = {
                x: -2,
                y: 0
            }
        }
        draw() {
          if (this.visible === true) {
            c.drawImage(this.image, this.position.x, this.position.y, this.width, this.height);
          }
        }
        update() {
            this.position.x += this.velocity.x;
            this.draw();
        }
    }
    let image = new Image()
    let imageTube = new Image()
    let imageBlock = new Image()
    image.src = 'https://samayass.github.io/samayaCSA/images/platform.png'
    imageTube.src = 'https://samayass.github.io/samayaCSA/images/tube.png'
    imageBlock.src = 'https://samayass.github.io/samayaCSA/images/box.png';
    //--
    // NEW CODE - ADD GOOMBA IMAGE
    //--
    let imageGoomba = new Image()
    imageGoomba.src = 'https://samayass.github.io/samayaCSA/images/goomba.png';
    let platform = new Platform(image)
    let tube = new Tube(imageTube)
    let blockObject = new BlockObject(imageBlock)
    let goomba = new Goomba(imageGoomba)
    player = new Player()
    let keys = {
        right: {
            pressed: false
        },
        left: {
            pressed: false
        }
    }
    function animate() {
        requestAnimationFrame(animate);
        c.clearRect(0, 0, canvas.width, canvas.height);
        platform.draw();
        player.update();
        tube.draw();
        blockObject.draw();
        //--
        // NEW CODE - UPDATE GOOMBA ANIMATION
        //--
        goomba.update();
        if (
            player.position.y + player.height <= blockObject.position.y &&
            player.position.y + player.height + player.velocity.y >= blockObject.position.y &&
            player.position.x + player.width >= blockObject.position.x &&
            player.position.x <= blockObject.position.x + blockObject.width
        )
        {
            player.velocity.y = 0;
        }
        if (keys.right.pressed && player.position.x + player.width <= canvas.width - 50) {
            player.velocity.x = 15;
        } else if (keys.left.pressed && player.position.x >= 50) {
            player.velocity.x = -15;
        } else {
            player.velocity.x = 0;
        }
        if (
                player.position.y + player.height <= platform.position.y &&
                player.position.y + player.height + player.velocity.y >= platform.position.y &&
                player.position.x + player.width >= platform.position.x &&
                player.position.x <= platform.position.x + platform.width
            )
            {
                player.velocity.y = 0;
            }
        if (
                player.position.y + player.height <= tube.position.y &&
                player.position.y + player.height + player.velocity.y >= tube.position.y &&
                player.position.x + player.width >= tube.position.x &&
                player.position.x <= tube.position.x + tube.width
            ) {
                player.velocity.y = 0;
                player.position.y += 0.1
                player.velocity.y = 0.0001
                gravity = 0.2
            }
            if (player.position.y + player.height == tube.position.y + tube.height ||
                    player.position.y + player.height <= tube.position.y ||
                    player.position.x + player.width <= tube.position.x ||
                    player.position.x >= tube.position.x + tube.width) {
                        gravity = 1.5
                    }
        if (
                player.position.x + player.width<= tube.position.x &&
                player.position.x + player.width + player.velocity.x >= tube.position.x &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
        if (
                player.position.x >= tube.position.x + tube.width &&
                player.position.x + player.velocity.x <= tube.position.x + tube.width &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
        if (
                player.position.x >= tube.position.x &&
                player.position.x + player.velocity.x <= tube.position.x &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
        if (
                player.position.x + player.width <= tube.position.x + tube.width &&
                player.position.x + player.width + player.velocity.x >= tube.position.x + tube.width &&
                player.position.y + player.height >= tube.position.y &&
                player.position.y <= tube.position.y + tube.height
            )
            {
                player.velocity.x = 0;
            }
            //--
            // NEW CODE - GOOMBA COLLISION DETECTION
            //--
        if(
            player.position.y + player.height <= goomba.position.y &&
            player.position.y + player.height + player.velocity.y >= goomba.position.y &&
            player.position.x + player.width >= goomba.position.x &&
            player.position.x <= goomba.position.x + goomba.width
        )
        {
            player.velocity.y = -20;
            goomba.visible = false;
            console.log(goomba.visible);
        }
        if (
            goomba.position.x >= platform.position.x &&
            goomba.position.x <= platform.position.x
        )
        {
            goomba.velocity.x = 2;
        }
        if (
            goomba.position.x + goomba.width <= tube.position.x &&
            goomba.position.x + goomba.width + goomba.velocity.x >= tube.position.x
        )
        {
            goomba.velocity.x = -2;
        }
    }
    animate();
    addEventListener('keydown', ({ keyCode }) => {
        switch (keyCode) {
            case 65:
                console.log('left');
                keys.left.pressed = true;
                break;
            case 83:
                console.log('down');
                break;
            case 68:
                console.log('right');
                keys.right.pressed = true;
                break;
            case 87:
                console.log('up');
                player.velocity.y -= 20;
                break;
        }
    });
    addEventListener('keyup', ({ keyCode }) => {
        switch (keyCode) {
            case 65:
                console.log('left');
                keys.left.pressed = false;
                break;
            case 83:
                console.log('down');
                break;
            case 68:
                console.log('right');
                keys.right.pressed = false;
                break;
            case 87:
                console.log('up');
                player.velocity.y = -20;
                break;
        }
    })
</script>