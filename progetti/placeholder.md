# New website

Date: 2025-08-28

---

My August has been spent relaxing and staying away from work and from computers as much as possible.
As I am gearing up to come back to the grind, I have decided to ramp things up gradually.
So I found myself rewriting my website from scratch, and here is the logbook.

### The problem

Up until now, I have been using the *very nice* [al-folio](https://github.com/alshedivat/al-folio) Jekyll template.
It is as fully-fledged as one may want.
In my case, however, it is a bit *too* complex.
I really only need a landing page with contacts, a list of papers I have worked on, and some super basic blog thing that supports maths typesetting, images and codeblocks.
Furthermore, in exchange for this plethora of possibilities, I had to keep a Jekyll toolchain around, as well as a Ruby installation.

I update this website way too infrequently to justify all of this toolchain-friction.
So I was looking for something a bit simpler.

### The requirements

Basically, I want to have a set of markdown files where I write down stuff and a very simple command that turns everything into a bundle of HTML files that are reasonably interlinked.
A lightweight system allows for quicker write-deploy cycles, so if rubbish appears in the deployed site I can fix it quickly.

### The tools

All of this has a solution: [pandoc](https://pandoc.org/) with some CSS template.
It plays nicely with [MathJax](https://www.mathjax.org/) for maths typesetting, and it is a tool I have used a lot in the past.
The secret sauce, then, is to ask Claude Sonnet 4 to come up with the skeleton.

### The result

Well, you are looking at the result right now.
The structure of the directory is the following:


```
website
├── Makefile
├── src/
│   ├── index.md
│   ├── template.html
│   ├── style.css
│   ├── blog.md
│   ├── papers.md
│   ├── blog/
│   │   ├── post1.md
│   │   └── post2.md
│   └── imgs/
│       ├── avatar.jpg
│       └── post1/
│           ├── img1.png
│           └── img2.png
└── build/
    ├── index.html
    ├── blog.html
    ├── papers.html
    ├── blog/
    │   ├── post1.html
    │   └── post2.html
    └── imgs/
        ├── avatar.jpg
        └── post1/
            ├── img1.png
            └── img2.png
```

Basically, ```build``` contains the HTML versions of the markdown files in ```src```, as specified by ```template.html``` and ```style.css```.

The secret sauce is then the ```Makefile```.
It basically calls ```pandoc``` with all the appropriate flags, copies files, and all that jazz.
It also deals with the maths typesetting.
Really sweet.

### Version control and deployment

The only ```git```-controlled folder is ```build```, which only contains HTML files.
Deployment happens by calling ```make deploy```, which adds-commits-pushes the changes in ```build``` to the Github pages repo.
The actual deployment is super quick, as all the HTML is ready to be displayed.

Let's see how long it takes for me to become unhappy at this system.
I am rather optimistic for now however.



