---
layout: post
title: "Quickest way to publish a personal blog with Jekyll"
description: "Today, I was searching for an easiest way to publish a personal blog. When I say easiest, I should be able to write, style and publish the blogs to a public domain effortlessly."
date: 2020-04-26 00:00:00
comments: true
image: https://miro.medium.com/max/700/1*PUsPnfjP14K8a5cCtFTWrQ.jpeg
keywords: "jekyll, Github Pages, Blogging, Personal Blog"
category: tech
tags:
- tech
---

Today, I was searching for an easiest way to publish a personal blog. When I say easiest, I should be able to write, style and publish the blogs to a public domain effortlessly.

## Jekyll and GitHub Pages

The search ended on Jekyll a static site generator. It has been around for quite sometime(since 2008). It works well with GitHub Pages and hence we can deploy it there without any hassle. Another advantage of using git for blogging is that we can treat it like any other code base.

## Let’s publish a blog

Familiarity with terminal, git and markdowns will definitely help you in this section, but that is not mandatory.
To start with the setup open a terminal window and follow the steps:

### Step 1: Install ruby

If you wish to keep multiple versions of ruby on your machine I suggest using [rvm](https://rvm.io/rvm/install), which is a ruby version manager. To install ruby and rvm:

```shell
$ \curl -sSL https://get.rvm.io | bash -s stable --ruby
```
To verify the ruby installation
```shell
$ ruby -v
```
### Step 2: Install Jekyll:
Get the value for `VERSION` from [here](https://pages.github.com/versions/).
```shell
$ gem install jekyll -v VERSION
```

### Step 3: Create a Jekyll project

Decide a name for your blog and create the Jekyll project. Since we are hosting it on GitHub Pages we can choose the name as <git-username>.github.io.
```shell
$ jekyll new riyasyash.github.io
```
This will create a new folder named `riyasyash.github.io` in the directory you ran the command from. This is the a template for a Jekyll project. cd to the directory and run `jekyll serve` . If everything is setup as expected you will be able to see the blog running on `http://localhost:4000`

<br>
<figure class="image"><center>
    <img src="https://miro.medium.com/max/700/1*MZfMf43O0y0YiiOAirA_-A.png" alt="{{ screenshot}}">
    <figcaption>{{ "screenshot" }}</figcaption>
</center>
  </figure>
<br>

### Step 4: Add a blog
Under your Jekyll project directory you can see a folder named `_posts` . This is where you should be adding all your blogs. You can see a sample blog there with examples of the templating (liquid) features it provides. You can find more about it [here](https://jekyllrb.com/docs/step-by-step/02-liquid/).

Now, replace this sample file with the content that you want to go on your blog. After that just refresh the site running on `http://localhost:4000` to see your changes.

### Step 5: Setup GitHub Pages Gem
Find the file named `Gemfile` in your project directory and change the line `gem “github-pages”, group: :jekyll_plugins` to `gem "github-pages", "~> VERSION", group: :jekyll_plugins` find the value for version from here. Also comment the line gem `“jekyll”, “~> 3.8.5”` .Run the following command to update the gem.
```shell
$ gem update github-pages
```
### Step 6: Push your project to GitHub
Head over to [GitHub](https://github.com/) and create a repository with your username like `<git-username>.github.io`

<br>
<figure class="image"><center>
    <img src="https://miro.medium.com/max/700/1*MvbkmzTvKWaDBFoXbwPgSQ.png" alt="{{ screenshot}}">
    <figcaption>{{ "screenshot" }}</figcaption>
</center>
  </figure>
<br>

To push the project run the following commands in your project directory
```shell
$ git init
$ git remote add origin https://github.com/riyasyash/riyasyash.github.io.git
$ git add .
$ git commit -m "initial commit"
$ git push -u origin master
```

If you go to the settings section in your GitHub repository you can see the link to your blog, which will look like this.

<br>
<figure class="image"><center>
    <img src="https://miro.medium.com/max/700/1*a0fvOZ_4VYklWlNc_t9X0w.png" alt="{{ screenshot}}">
    <figcaption>{{ "screenshot" }}</figcaption>
</center>
  </figure>
<br>

click on the link and just like that your personal blog is live. 🎉

### Step 7: Beautify your blog

Let’s personalize and beautify the blog a little more. Open the file `_config.yml` in your project and edit the fields title,email,description and social usernames according to your need. You can also optionally choose a theme from here, but be mindful about the layouts in the theme. Once you are done add the files and push them to git.
```shell
$ git add .
$ git commit -m "personalized variables"
$ git push
```
This will automatically update your blog in the GitHub pages (Yes, it is that easy). Whenever you have to add a new blog just add it to the _posts folder and push to git.
That is it, Happy Blogging !