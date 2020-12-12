---
layout: post
title:  "Python modules and virtualenv"
date:   2020-12-12 00:17:08 -0700
---

Over the past few months I had to setup a few pythons code bases for my projects and I decided to try to do it the right way -- or at least a cleaner way than usual.

### Virtual environments and custom Python modules
I'll skip the pitch for virtual environments, a Google search can give [stackoverflow explanations](https://stackoverflow.com/questions/41972261/what-is-a-virtualenv-and-why-should-i-use-one) or more extensive [blog posts](https://realpython.com/python-virtual-environments-a-primer/). Instead I'll outline some of the steps I followed on getting virtual environments properly setup. For my use case, I wanted to setup an environment where I could use my custom Python modules without adding it to my global Python path. Typically in a virtual environment you can use pip to install released Python packages; this will automatically handle adding dependencies to your local site-packages (more will follow). However, if you want to use a custom Python module you're developing from anywhere within your virtualenv.

#### First (cleaner) approach
On a fresh machine I used the "cleaner" approach to setup my virtual environment. I was specifically working with python3, so I made sure to enforce usage of python3 modules by pre-pending `python3 -m` to all my commands. First things first, installing virtualenv:
```
python3 -m pip install --user virtualenv
python3 -m venv venv
```

Now I have my virtual environment setup. Let's say my directory structure is as such
```
.
+-- venv
+-- module_one
|   +-- __init__.py
|   +-- module_one
+-- module_two
|   +-- __init__.pyt
|   +-- module_two
+-- scripts
|   +-- script.py
```

and that my script.py depends on both module_one and module_two. Running it, even without the virtual environment, won't work because Python doesn't know where to find module_one and module_two. Instead, you'll need to add the path to your modules in your virtual environment's site-packages directory. I followed this [stackoverflow post](https://stackoverflow.com/questions/10738919/how-do-i-add-a-path-to-pythonpath-in-virtualenv), but basically you'll want to add a .pth file in venv/lib/python3.6/site-packages/ that is the path to your module dependency:
```
echo /path/to/repo/module_one > venv/lib/python3.6/site-packages/module_one.pth
```

Now, if you enter your virtual environment `source venv/bin/activate` your script should be able to find your module dependencies!

#### Second approach (not as clean)
On a separate machine, I was not able to use this approach because I had already made manual adjustments to my user pythonpath. Generally, this is ill-advised, but since I couldn't quite remember why I would have wanted to do that and didn't want to risk breaking other existing projects I needed to find an alternative approach. In this particular case, my application was a bit more specific than just using a module within a particular repo's virtual environment. Rather, I had wanted to setup dependencies between two of my repos. In a future blog post I might talk about how to do this via the use of [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules). In this case though, I actually modified my local user site-packages directory following this [stackoverflow post](https://stackoverflow.com/questions/16196268/where-should-i-put-my-own-python-module-so-that-it-can-be-imported). Honestly, where would we be without stackoverflow. The short of it is that I created a symbolic link within my python3.6 site-packages to my module (note, this is the folder that has the \_\_init\_\_.py file).
```
ln -s /path/to/repo/module_one ~/.local/lib/python3.6/site-packages/module_one
```

Hope this helps! Feel free to ping with any revisions or suggestions. Stay tuned for some upcoming posts about Python unit testing using nose and setting up some git bash niceties in your terminal, and maybe some other stuff.