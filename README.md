# My tiny little 1 bit Universe

My tiny little 1 bit universe is a thought experiment on entropy. We create a simple universe. Our universe is just a bit string. Of course, we want a infinite universe so it is an infinite bit string. We want to run our universe on a regular laptop. So we start with a completely empty universe.

```javascript
function stateAt(position){
  return 0;
}
```

You might say our universe is boring, but it is infinite. Let's add a particle at a random position.
Shot. Its position is almost infinitely large. We can not represent that on my laptop. 
Let's cheat a little and introduce a camera to our universe. 
We center our camera at the position of the "big bang" -- that's where our random particle occured.
We take that for granted and describe the universe relatively to the position of the camera.

```javascript
function stateAtCamera(relativePosition){
  if(relativePosition == 0){
    return 1;
  } else {
    return 0;
  }
}
```

That's neat. Now we are able to run our little infinite universe on our computer again. Yet, it is still hyper boring. Our particle is just at position 0 and it never moves. 

We need time. We introduce time steps. Still, the particle doesn't move. Hmn... It needs a velocity, such that it has a different position at the next time step. Cool. Though the velocity must be limited. Otherwise the position of the particle exceeds our laptop's memory. Let's call the maximum velocity `c`.  At every time step, the particle can change its position at most `c` steps to the left or right. We dumb it down to `c=1`.

We define our universe to be completely non-deterministic. Our particle changes its velocity randomly at every move.

```javascript
let currentPosition = 0;

function timeStep(){
  if( Math.random() > 0.5 ){ // random movement 
    currentPosition += 1;    // to the right 
  } else {
    currentPosition -= 1;    // to the left
  }
}

function stateAtCamera(relativePosition){
  if(relativePosition == currentPosition){
    return 1;
  } else {
    return 0;
  }
}
```

We could represent the history of the universe as a bit string. It represents the particle's sequence of moves to the left or right. At every point in time we require one more bit. 
