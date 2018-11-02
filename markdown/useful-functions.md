# Useful Functions

Here are some functions that can be useful when creating a jupyter notebook.

## Table of contents
1. [Including Images](##including-images)
2. [Including Youtube videos](##including-youtube-videos)
3. [Inlcuding Geogebra applications](##including-geogebra-applications)
4. [Including WebGl animations](##including-webgl-animations)
5. [Including Music and Sounds](##inclusing-music-and-sounds)
6. [Creating Synthetic sounds](##creating-synthetic-sounds)
7. [Creating simple plots](##creating-simple-plots)
8. [Creating 3D plots](##creating-3d-plots)
9. [Creating Animated plots](##creating-animated-plots)
10. [Using widgets](##using-widgets)
11. [Drawing in HTML and SVG](##drawing-in-html-and-svg)
12. [Hiding code](##hiding-code)
13. [Saving work to Github](##saving-work-to-github)




## Including Images

You can include local or remote image within a Jupyter notebook in two ways.

1. Markdown Syntax: To include an image in a markdown cell use below syntax, start with an exclamation point, then include text and file names in square and curved brackets. The text is the square brackets is loaded only if the computer can't find the image file or if the link to the remote file is broken.

    `![Any text here](yourImager.jpg)`

2. HTML syntax: This syntax can be used when you need to have more control over how you display the image.

    `<img src="yourImage.jpg" alt="Alternate text" width="200"/>`


## Including Youtube videos

When you find any Youtube videos that you would like to include in your Jupyter notebook, get the web reference by clicking on the share button and you use that in the code cell using the code below.

    ```python
    from IPython.display import YouTubeVideo
            YouTubeVideo('ZmhlRsYjs7Y')```

or

Get the iframe command by clicking on the "Embed" option on the Youtube webpage and use it in a code cell.

```
%%html
<iframe width="300"  src="https://www.youtube.com/embed/ZmhlRsYjs7Y?start=30" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
```

## Inlcuding Geogebra applications

To include a Geogebra application in a Jupyter noteobook.

Step 1: Create your app in the Geogebra.org website, then export it as a .ggb file 
Step 2: Upload the file into the Jupyter notebook
Step 3: Set up initialization by adding this command in a code cell and running it.
        ```
        %%html
        <script src="https://cdn.geogebra.org/apps/deployggb.js"></script>
        ```
Step 4: Then read in the file using the command.
        ```
        <script>
        var ggbApp = new GGBApplet({
            "height": 400,
            "showToolBar": false,
            "showMenuBar": false,
            "showAlgebraInput": false,
            "showResetIcon": true,
            "enableLabelDrags": false,
            "enableRightClick": false,
            "enableShiftDragZoom": true,
            "useBrowserForJS": false,
            "filename": "Your-ggb-file.ggb"
            }, 'ggb-point');
        ggbApp.inject();
        </script>
        ```


## Including WebGl animations

 You can use HTML magic and iframes to include WebGl animations like below:

```
 %%html
<iframe src="webgl-file-name.html" width="500" height=500></iframe>
```

## Including Music and Sounds

You can upload .wav or .mp3 like data files onto the Jupyter hub account or use the URL of a remote sound file and include it in the Jupyter notebook using these code blocks below:

HTML magic: (Source can either be a local file name or link to a remote file)

```
%%html
<audio controls>
  <source src="your-sound-file.wav" type="audio/wav">
Your browser does not support the audio element.
</audio>
```
or

Python tool: (Source can either be a local file name or link to a remote file)

```python 
from IPython.display import Audio  ## only import once per notebook
    Audio(data='https://ccrma.stanford.edu/workshops/mir2014/audio/T37-vibraphone-8k.wav')
```

## Creating Synthetic sounds

To create and play sound in a Jupyter noteboook, we run the following two tools.
```python
from numpy import *    ## for numerical functions
from IPython.display import Audio  ## to output audio
```
Let's just create a list of random numbers and use the Audio tool to create random noise, the computer will translate these numbers into an electrical signal that is sent to computer's speaker.

```python
Fs = 8000
signal = random.randn(Fs)

Audio(data=signal, rate=Fs)
```
Play around with 

## Creating simple plots

### matplotlib
To plot with matplotlib we'll have to load the "pyplot" module and it is important to tell the notebook that you want your plots to appear "inline", which is to say they will appear in a cell inside your notebook. Run the following two commands to get it setup:

```python
%matplotlib inline
from matplotlib.pyplot import *
```

To draw a simple line plot with five data points, run the command as follows.

```python
plot([1,2,2,3,5]);
```
To plot those data points again but marked with circles, run the command that follows:

```python
plot([1,2,2,3,5],'o');
```

To plot a bar chart with x and y axes. Try this:

```python
x = [1,2,3,4,5]
y = [1,2,2,3,5]
bar(x,y);
title("Hey, this is my bar chart");
xlabel("x values");
ylabel("y values");
```

### Plotly
Plotly offline allows you to create graphs offline and save them locally. 

There are two ways you could plot offline:

1. plotly.offline.plot(): to create and standalone HTML that is saved locally and opened inside your web browser.

2. plotly.offline.iplot(): when working offline in a Jupyter Notebook to display the plot in the notebook

Here is an example of how you can plot inline in a Jupyter notebook. First we'll have to import plotly.offline and graph_objs module and call the plotly.offline. The `init_notebook_mode(connected=True)` will initiate the plotly notebook mode which allows you to use plotly.offline. Then finally use iplot to inject the plotly.js source file containing the data and layout into the notebook.

```python 
from plotly.offline import init_notebook_mode, iplot
import plotly.graph_objs as go

init_notebook_mode(connected=True)

iplot({
    "data": [go.Scatter(x=[1, 2, 3, 4], y=[4, 3, 2, 1])],
    "layout": go.Layout(title="hello world")
}, auto_open=True)
```

## Creating 3D plots

### matplotlib3

To use matplotlib3 to create 3D plots we will first import all the necessary tools:

```python
%matplotlib inline
from mpl_toolkits.mplot3d import Axes3D
from matplotlib.pyplot import *
from numpy import *
```
Let us try to draw a simple hyperboloid which comes from the equation: $$z = x^2 - y^2.$$

The key idea is to define a range of values for variables x and y, combine them as a "meshgrid" which is just an array of values, then evaluate the quadratic above to give the z values.

From this data, we then create the 3D figure and plot. 

```python

# Make data.
X = [-2,-1,0,1,2]
Y = [-2,-1,0,1,2]
X, Y = meshgrid(X, Y)
Z = X**2 - Y**2

# create the 3D figure
fig = figure()
ax = fig.gca(projection='3d')


# Plot the surface.
surf = ax.plot_surface(X, Y, Z,
                       linewidth=0, antialiased=False)
```

More information on 3D plotting here: https://matplotlib.org/mpl_toolkits/mplot3d/tutorial.html

### Plotly

Plotly allows us to create interactive 3D plots. To create a simple plot let us first load in the modules and create the data to plot. We create an array of z values -- these will be heights in the surface plot. Then we make three surfaces by adding a constant to z. This is fed into our data structure, and plot the result.

```python
from plotly.offline import init_notebook_mode, iplot
import plotly.graph_objs as go

init_notebook_mode(connected=True)

z1 = [
    [8.83,8.89,8.81,8.87,8.9,8.87],
    [8.89,8.94,8.85,8.94,8.96,8.92],
    [8.84,8.9,8.82,8.92,8.93,8.91],
    [8.79,8.85,8.79,8.9,8.94,8.92],
    [8.79,8.88,8.81,8.9,8.95,8.92],
    [8.8,8.82,8.78,8.91,8.94,8.92],
    [8.75,8.78,8.77,8.91,8.95,8.92],
    [8.8,8.8,8.77,8.91,8.95,8.94],
    [8.74,8.81,8.76,8.93,8.98,8.99],
    [8.89,8.99,8.92,9.1,9.13,9.11],
    [8.97,8.97,8.91,9.09,9.11,9.11],
    [9.04,9.08,9.05,9.25,9.28,9.27],
    [9,9.01,9,9.2,9.23,9.2],
    [8.99,8.99,8.98,9.18,9.2,9.19],
    [8.93,8.97,8.97,9.18,9.2,9.18]
]

z2 = [[zij+1 for zij in zi] for zi in z1]
z3 = [[zij-1 for zij in zi] for zi in z1]

data = [
    go.Surface(z=z1),
    go.Surface(z=z2, showscale=False, opacity=0.9),
    go.Surface(z=z3, showscale=False, opacity=0.9)

]

iplot(data)
```

## Creating Animated plots

### matplotlib

Matplotlib come with a rich collection of tools to allow us to make movies. Below, you'll see an example of how you can make a simple animated plot using matplotlib.

As always we'll first load the necessary modules,

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from IPython.display import HTML
```

Then using subplot we create a figure object, and two functions `init`, which sets up the y-data in the plot and `animate`, which defines the data for the series of plots we want to display. 

Now lets try plotting the translates of the sine function. Animate(i) uses the variable i to count frames, and that i value determines how much we translate the sine function by.

In this example, i will range from 0 to 99, giving a full cycle of the sine function.

```python

fig, ax = plt.subplots()

x = np.arange(0, 2*np.pi, 0.01)
line, = ax.plot(x, np.sin(x))


def init():  # only required for blitting to give a clean slate.
    line.set_ydata([np.nan] * len(x))
    return line,


def animate(i):
    line.set_ydata(np.sin(x + i / 100))  # update the data.
    return line,
```

Next, we call the animation function as follows, making use of the figure, init and animate functions defined above. This creates a new data object call "ani" which holds the movie.

```python
ani = animation.FuncAnimation(
    fig, animate, init_func=init, interval=2, blit=True, save_count=50)
```

Finally, we display the movie using the HTML() command from the module IPython.display.
```python
HTML(ani.to_html5_video())
```

A simple "save" command turns the animation into an mp4 movie file, that you can use elsewhere. 

```python
ani.save("movie.mp4")
```

We can play the saved movie directly in html using:

```python
%%html
<iframe src="movie.mp4"></iframe>
```

### D3

D3 is a great tool to create animations.

To create animations with D3 we'll first have to bypass a security issue with Jupyter notebook. Jupyter notebook has security measures in place to avoid what it suspects might be malicious (dangerous) code. To get your notebook tobypass the security: we write the Javascript code in the notebook, then save it as a .html file. We then use some Python code to load in this .html code. 

First lets load the IFrame tool which will be used to display the animation encoded in the .html file.

```python
from IPython.display import IFrame
```

**Next,** we create a file called myFile.html, and write the following Javascript code into the file. 

This .html file is rather complex. Main things to notice is that in the <head> section, it loads in the D3 code from a remote site. In the <body> section, it creates an svg canvas where the animation will happen. The animation involves a bunch of balls that bounce into each other. 

```html
%%writefile myFile.html
<!DOCTYPE html>
<html>
<head>
    <script src="//cdnjs.cloudflare.com/ajax/libs/d3/4.8.0/d3.min.js"></script>
    <script src="//unpkg.com/d3-force-bounce"></script>
    <script src="//unpkg.com/d3-force-constant"></script>
</head>

<style>
body {
    margin: 0;
    text-align: center;
}

.ball {
    cursor: grab;
    cursor: -webkit-grab;
}

.ball:active {
    cursor: grabbing;
    cursor: -webkit-grabbing;
}
</style>

<body>
    <svg id="canvas">
        <defs>
            <radialGradient id="sphere-gradient">
                <stop offset="0%" stop-color="MediumPurple"></stop>
                <stop offset="100%" stop-color="Indigo"></stop>
            </radialGradient>
        </defs>
    </svg>
</body>

<script>

var width = 400, height = 400
const BALL_SIZE = 20,
	BALL_OFFSET = window.innerHeight/8,
	BALL_SPEED = 3;

const canvasWidth = window.innerWidth,
	canvasHeight = window.innerHeight;

// DOM nodes
const svgCanvas = d3.select('svg#canvas')
		.attr('width', canvasWidth)
		.attr('height', canvasHeight),
	wiresG = svgCanvas.append('g'),
	ballsG = svgCanvas.append('g');

const balls = [
		{ id: '0', init: { x: canvasWidth/2 - 6*BALL_SIZE, y: canvasHeight*1/3, vx: 0, vy: 0 } },
		{ id: '1', init: { x: canvasWidth/2 - 3*BALL_SIZE, y: canvasHeight*(1/3 + .01), vx: 0, vy: 0 } },
		{ id: '2', init: { x: canvasWidth/2 - 0*BALL_SIZE, y: canvasHeight*1/3, vx: 0, vy: 0 } },
		{ id: '3', init: { x: canvasWidth/2 + 3*BALL_SIZE, y: canvasHeight*1/3, vx: 0, vy: 0 } },
		{ id: '4', init: { x: canvasWidth/2 + 6*BALL_SIZE, y: canvasHeight*1/3, vx: 0, vy: 0 } }
	];

	// start the left ball moving
	balls[0].init.x -= BALL_OFFSET;
	balls[0].init.y -= 0;
    balls[0].init.vx = BALL_SPEED;

let init = false;

const forceSim = d3.forceSimulation()
	.alphaDecay(0)
	.velocityDecay(0)
	.nodes([...balls])
	.force('elastic', d3.forceBounce()
		.radius(node => BALL_SIZE)
        .elasticity(1)
	)
	.force('init', () => {
		if (!init) {
			balls.forEach((ball) => {
				ball.x = ball.init.x;
				ball.y = ball.init.y;
				ball.vx = ball.init.vx;
				ball.vy = ball.init.vy;
			});
			init = true;
		}
	})
	.on('tick', () => { ballDigest(); });

//

// Periodical kickstart
kickStart();
setInterval(kickStart, 5000);

function ballDigest() {
	let ball = ballsG.selectAll('circle.ball').data(balls);

	ball.exit().remove();

	ball.merge(
		ball.enter().append('circle')
			.classed('ball', true)
			.attr('r', BALL_SIZE)
			.attr('fill', 'url(#sphere-gradient)')
			.call(d3.drag()
				.on("start", d => { d.fx = d.x; d.fy = d.y; })
				.on("drag", d => { d.fx = d3.event.x; d.fy = d3.event.y; })
				.on("end", d => { d.fx = null; d.fy = null; })
			)
	)
		.attr('cx', d => d.x)
		.attr('cy', d => d.y);
}

function kickStart() {
			balls.forEach((ball) => {
				ball.x = ball.init.x;
				ball.y = ball.init.y;
				ball.vx = ball.init.vx;
				ball.vy = ball.init.vy;
			});
}


  </script>
</html>
```

Finally, we call us IFrame to load in the .html file and make it run.

```python
IFrame('myFile.html',500,500)
```
## Using widgets

Widgets are a quick way to get interactivity in your Jupyter displays. They include graphical user interface tools like sliders, check boxes, and more. 

We use interact tool to access the Jupyter's own version of Python widgets. 

First we import the interact tool:
```python
from ipywidgets import interact
```
Then define a simple function that the widgets will activate.

```python
def f(x):
    return x
```
Next, we create the widgets by calling the interact function, using an argument type for x.

The choice of x will give us sliders with integer or float values, check boxes, or text entry boxes. You can try each of the following:

```python
interact(f,x=(0,10));
```

## Drawing in HTML and SVG

Sometimes we just need a quick drawing within a Jupyter notebook. A quick way to do this is in an HTML cell, using Scalable Vector Graphics elements (or SVG).

The idea is straightforward. We create an html cell, put an svg canvas in it, then draw some objects in it. Here are two simple examples. 

Here we set up an svg canvas of size 100x100, and draw a circle in it. Note how we set the position and radius of the circle. 

```html
%%html
<html>
<body>

<h1>My first SVG</h1>

<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
</svg>

</body>
</html>
```


## Hiding code

It is sometimes useful to hide code to make the presentation less cluttered and less confusing to the viewer. The following piece of code, once run, creates a "Show code / Hide code" button in the notebook, that will display or hide code as per your selection.

You can copy this code into your own notebooks, to add this functionality whenever you want it.

Run the following block, and click the button to see how it works.

```html
%%html

<script>
  function code_toggle() {
    if (code_shown){
      $('div.input').hide('500');
      $('#toggleButton').val('Show Code')
    } else {
      $('div.input').show('500');
      $('#toggleButton').val('Hide Code')
    }
    code_shown = !code_shown
  }
  
  $( document ).ready(function(){
    code_shown=false;
    $('div.input').hide()
  });
</script>
<form action="javascript:code_toggle()"><input type="submit" id="toggleButton" value="Show Code"></form>
```

## Saving work to Github

Saving your work on Github

Here are the key steps. Run all these command in a new Terminal in your Jupyter Hub. Change directories until you are in the directory (folder) that you want to save on GitHub.

    If you haven't set up your name and email for git yet, you need to do that:

    `git config --global user.email "you@example.com"`
    `git config --global user.name "Your Name"`

    From inside the folder you want to save, set it up as a git repo with these commands:

    `git init`
    `git add *`
    `git commit -m "First commit, or whatever"`

    Log onto Github, on your account, and create a new repo. Here, we call it Test1. DO NOT include any initialization files.

    Add your github account repo as the origin for your local repo. (Here, acct_name should be replaced with your github account. Test1.git is the name of the github repo you created.)

    `git remote add origin https://github.com/acct_name/Test1.git`

5. Now push your local files onto the github repo using this:

    `git push -u origin master`

    Git will ask you for your github account name and password, before proceeding.

    You can now check on GitHub to see that your online repo has been populated with the files you wanted.

    From now on, you can pull and push items between your local repo and the Github repo as you desire.

