# My tiny little infinite Universe

My tiny little infinite universe is a thought experiment on entropy. We create a simple universe. Our universe is just a bit string. Of course, we want to have an infinite universe so it is an infinite bit string. We want to run our universe on a regular laptop. So we start with a completely empty universe.

```javascript
function stateAt(position){
  return 0;
}
```

You might say our universe is boring, still it is infinite. Lots of stuff can happen in an infinite universe. It is so insanely huge, that a particle might occur at a random position. Shoot! Its position is almost infinitely large. Even Billions of Gigabytes would not be enough to encode the particle's position. We can not represent that on my laptop. 
We have to cheat a little and introduce a camera to our universe. 
We center our camera at the position of the "big bang", where our random particle occured.
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

We could represent the history of the universe as a bit string, representing the particle's sequence of moves to the left or right. At every point in time we require one more bit. The entropy of our universe's history increases by 1 bit per time step.

More interesting is the information required to represent the current state of our universe. Naively we could say, that at every time step `currentPosition` requires 2 bits more, because in the worst case the particle could have moved always left or always right. That's wrong though. The particle follows a binominal distribution with `p=0.5` and `n= #timeSteps`. At every point in time the standard deviation grows.





