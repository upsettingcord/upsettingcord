Ok so this is a Snake game. When you code it in your Text Editor save it with a .html extension.
If you've had a phone in the early 2000s you probably know snake that you would play on yours or your mums nokia brick
by upsettingcord
ok broskis the rule and how the game work is
you gotta eat the blue as it is food. 
You grow when you eat 
If you hit yourself by going into 
the wall then back out on the other side
then you get smaller
or if you go up then back down and fly into yourself you get smaller
Code below |
           |
          \ /

<html>
    <head>
	<title>SnakeGame </title>
	
	 </head>
	 
	 <body>



<canvas id=canvas height=400 width=600>
</canvas>

<script>

function Game(){
  this.snake = new Snake();
  this.food = new Food();

  this.ctx = canvas.getContext('2d');
  this.scale = 20;
  this.nx = Math.floor(canvas.width/this.scale);
  this.ny = Math.floor(canvas.height/this.scale);

  this.step = function(){
    this.snake.step(this);
    this.food.step(this);

    this.draw();
    this.wait();
  };
  this.draw = function(){
    this.Rect(0, 0, this.nx, this.ny, '#AAAAAA');

    this.snake.draw(this);
    this.food.draw(this);
  };
  this.keydown = function(evt){
    this.snake.keydown(evt.key);
  }

  this.Rect = function(x,y,w,h,fs){
    this.ctx.fillStyle = fs;
    this.ctx.fillRect(x*this.scale, y*this.scale, w*this.scale-1, h*this.scale-1)
  };

  this.wait = function(){
    setTimeout(this.step.bind(this), 1000/25);
  };

  document.addEventListener('keydown', this.keydown.bind(this));
  this.wait();
}

function Snake(){
  this.l = 2;
  this.trace = [];
  this.x = 10;
  this.y = 10;
  this.vx = 1;
  this.vy = 0;

  this.step = function(game){
    this.x = this.x + this.vx;
    this.y = this.y + this.vy;

    if(this.x >= game.nx) this.x = 0;
    if(this.y >= game.ny) this.y = 0;
    if(this.x < 0 ) this.x = game.nx - 1;
    if(this.y < 0 ) this.y = game.ny - 1;

    for(var i=0; i<this.trace.length; i++){
      var pos = this.trace[i];
      if( pos.x == game.food.x && pos.y == game.food.y ){
        this.l = this.l + 1;
        game.food.reset(game);
      }

      if(pos.x == this.x && pos.y == this.y) this.l = 2;
    }

    this.trace.push({x: this.x, y: this.y});
    while(this.trace.length > this.l) this.trace.shift();
  };
  this.draw = function(game){
    for(var i=0; i<this.trace.length; i++){
      var pos = this.trace[i];
      game.Rect(pos.x, pos.y, 1, 1, 'white');
    }
  };
  this.keydown = function(key){
    if(key == 'ArrowDown'){
      this.vx = 0;
      this.vy = 1;
    } else if(key == 'ArrowUp'){
      this.vx = 0;
      this.vy =-1;
    } else if(key == 'ArrowLeft'){
      this.vx =-1;
      this.vy = 0;
    } else if(key == 'ArrowRight'){
      this.vx = 1;
      this.vy = 0;
    }
  };
}

function Food(){
  this.x = 3;
  this.y = 4;
  this.step = function(game){};
  this.draw = function(game){
    game.Rect(this.x, this.y, 1, 1, 'blue');
  };

  this.reset = function(game){
    this.x = Math.floor(Math.random()*game.nx);
    this.y = Math.floor(Math.random()*game.ny);
  };
}


window.onload = function(){
    new Game();
};
</script>
<head>Rules</head>
    </body>
</html>
