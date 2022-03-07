# My Tiny Little Infinite Universe

*My tiny little infinite universe* is a thought experiment on entropy. We create a simple universe. Our universe is just a bit string. Of course, we want to have an infinite universe so it is an infinite bit string. We want to run our universe on a regular laptop. So we start with a completely empty universe because we can represent it easily:

```javascript
function stateAt(position){
  return 0;
}
```

You might say our universe is a bit boring, still it is infinite and runs on our computer. Lots of stuff can happen in an infinite universe. It is so insanely huge, that a particle might occur at a random position... Shoot! There's a particle but its position is almost infinitely large. Even billions of gigabytes would not be enough to encode the particle's position. We can not represent that on my laptop. 
We have to cheat a little and introduce a camera to our universe. 
We center our camera at the position of the "big bang", where our random particle occurred.
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

That's neat. Now we are able to run our little infinite universe on our computer again. Yet, I admit, it is still hyper boring... Our particle is always at position 0 and it never moves. 

We need time. We introduce time steps. Still, the particle doesn't move. Hmn... It needs a velocity, such that it has a different position at the next time step. Cool. Though the velocity must be limited. Otherwise the position of the particle exceeds our laptop's memory. Let's call the maximum velocity `c`.  At every time step, the particle can change its position at most `c` steps to the left or right. We dumb our model down to `c=1`.

We define our universe to be completely non-deterministic. Our particle changes its velocity randomly at every move.

```javascript
let currentPosition = 0;
let t = 0;

function timeStep(){
  if( Math.random() > 0.5 ){ // random movement 
    currentPosition += 1;    // to the right 
  } else {
    currentPosition -= 1;    // to the left
  }
  t += 1;                    // increment the time
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
```
history = t * 1 bit
```

More interesting is the information required to represent the current state of our universe. Naively we could say, that at every time step `currentPosition` requires `2*log2(t) bits`, because in the worst case the particle could have moved always left or always right. The actual entropy is lower though. The particle follows a binomial distribution with 
```
p = 0.5 
n = 2 * t
```
At every point in time only the standard deviation grows. The [entropy of a variable that is binomially distributed](https://math.stackexchange.com/questions/244455/entropy-of-a-binomial-distribution) is about

```
E(n,p) = 1/2 log2( 2π e n p q ) + 𝓞(1/n) bits
```

Simplifying, with `p=1/2`, `q=1-p`, etc
```
E(n) = 1/2 log2( 2π e n p (1-p) ) + 𝓞(1/n) bits
     ~ 1/2 log2( 2π e n 1/4 ) bits
     = 1/2 log2( π e n / 2 ) bits
```

Substituting `t = n/2` shows the entropy of our universe grows over time like:
```
E(t) = 1/2 log2( π e t ) bits
```




## Further Thoughts 
- The algorithmic complexity of any deterministic universe is constant. All information follows from its laws and the initial configuration.
- The algorithmic complexity of any multi-particle, expanding, almost-deterministic universe is much much lower than its Shannon entropy. 
- The algorithmic complexity of any universe with a mind that has a free will increases with every decision of that mind.
