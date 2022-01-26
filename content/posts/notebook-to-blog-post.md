---
categories: ["blog"]
date: "2021-07-16T12:11:29+05:30"
description: "Quick set of instructions to convert a Jupyter notebook to a hugo blog post."
draft: false
tags: ["markdown", "jupyter", "hugo"]
title: "Convert Jupyter Notebook to Hugo Blog Post"

---

## How to convert a Jupyter Notebook to Hugo Blog

We can use `nb2hugo` to convert Jupyter notebooks to a Hugo markdown blog. The home page for [nb2hugo](https://github.com/vlunot/nb2hugo/) has more details about this. There is also another [blog post](https://skeptric.com/jupyter-hugo-blog/) that kind of shows how to use it.

Here the steps involved in doing this conversion. 

1. Copy over the notebook to the hugo blog repo in the `notebook` directory. I think there is some flakiness with respect to names in capital, so recommend keeping all names to lowercase and using `-` as the word separator. 
2. Even though the `nb2hugo` website recommends creating the metadata in the jupyter notebook, I have had trouble with it. I have been adding the metadata to the generated markdown file after the process completes.
3. Run the below commnand to convert the notebook to the blog. 
```
nb2hugo notebook/plotting-using-matplotlib.ipynb --site-dir ./ --section posts
```
4. You might have to adjust the path to the images within the markdown file. By default the `.md` file gets created in the `${HUGO_ROOT}/content/posts` assuming that the section in the command above was posts. The images get copied over to `${HUGO_ROOT}/static/posts/<post-title-name>/`. It should work by default, but in case it doesn't, please adjust the path to the images.  In general the path to `${HUGO_ROOT}/static/posts/Plotting-using-Matplotlib/output_4_0.png` should be updated to `/posts/Plotting-using-Matplotlib/output_4_0.png`. As said before this should work be default and might need to be updated only if really required.

