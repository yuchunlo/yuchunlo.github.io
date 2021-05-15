---
layout: default
title: Simple randomness generation
description: Get a random item in JavaScript and Python.
date: 2021-05-15
permalink: /simple-randomness-generation/
---

> The epiphany I had in my career in randomness came when I understood that I was not intelligent enough, nor strong enough, to even try to fight my emotions. Besides, I believe that I need my emotions to formulate my ideas and get the energy to execute them.
> I am just intelligent enough to understand that I have a predisposition to be fooled by randomness—and to accept the fact that I am rather emotional. I am dominated by my emotions—but as an aesthete, I am happy about that fact.
> – Nassim Nicholas Taleb, *Fooled by Randomness: The Hidden Role of Chance in Life and in the Markets*

To sample without replacement in Python:

```python
import numpy as np
n = 7
N = np.random.choice(n, n, replace=False)
```

For sampling an item from a dictionary `strDict` in JavaScript, and display the random string to `output` and image to `img` in HTML.

```javascript
function getRandomInt(min, max) {
  min = Math.ceil(min); 
  max = Math.floor(max); 
  return Math.floor(Math.random() * (max - min) + min); // the maximum is exclusive and the minimum is inclusive
}; 

function getRandomStr() {
  if (Object.keys(strDict).length < 1) {
    document.getElementById('output').innerHTML = 'End.'; 

    // remove images and buttons
    document.getElementById('img').remove(); 
    buttons = document.getElementsByTagName('button'); 
    while (buttons[0]) buttons[0].parentNode.removeChild(buttons[0]); 

    const refreshBtn = document.createElement('button'); 
    refreshBtn.innerHTML = 'Refresh'; 
    refreshBtn.className = 'btn btn-success btn-lg btn-block'; 
    refreshBtn.addEventListener ('click', function refreshPage() {
      location.reload(); 
    }); 
    body.appendChild(refreshBtn); 
  }
  else {
    rNum = getRandomInt(0, Object.keys(strDict).length); 
    rStr = Object.keys(strDict)[rNum].replace(/\n/g, '<br>'); 
    document.getElementById('output').innerHTML = rStr; 
    document.getElementById('img').setAttribute('src', Object.values(strDict)[rNum]); 
    delete strDict[Object.keys(strDict)[rNum]]; 
  }; 
}; 
```

Here is the demo:
{% include quote-randomness-js.html %}
