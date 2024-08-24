Skip to content
DEV Community
Find related posts...
Powered by  Algolia
Log in
Create account

44
Jump to Comments
79
Save

Cover image for How to enable GitHub Actions on your Profile README for a snake-eating contribution graph 🐍
Michelle Duke
Michelle Duke
Posted on Jun 28, 2021 • Updated on Feb 22


173

11
How to enable GitHub Actions on your Profile README for a snake-eating contribution graph 🐍
#
github
#
markdown
#
opensource
#
tutorial
GitHub Like a Boss (23 Part Series)
1
GitHub Desktop for better repo organisation
2
GitHub README for easy to understand code
...
19 more parts...
22
How to automatically close your issues once you merge a PR
23
How to get more suggestions from GitHub Copilot
Lots of people have been talking about and sharing their GitHub Profile READMEs. It was a project we launched last year and developers are loving it. As this feature became more popular, more developers were building templates, plugins, and apps for you to use on your profile.

This post from Supritha caught my attention. I like the way they talk about various pieces of code to have on your GitHub Profile README.

supritha 
How to have an awesome GitHub profile ?
Supritha ・ Jun 8 '21
#github #markdown #opensource #git
One of the comments from Guillaume Falourd pointed to a really cool project from Platane.

GitHub logo Platane / snk
🟩⬜ Generates a snake game from a github user contributions graph and output a screen capture as animated svg or gif
snk
GitHub Workflow Status GitHub release GitHub marketplace type definitions code style

Generates a snake game from a github user contributions graph

github contribution grid snake animation
Pull a github user's contribution graph Make it a snake Game, generate a snake path where the cells get eaten in an orderly fashion.

Generate a gif or svg image.

Available as github action. It can automatically generate a new image each day. Which makes for great github profile readme

Usage
github action

- uses: Platane/snk@v3
  with
    # github user name to read the contribution graph from (**required**)
    # using action context var `github.repository_owner` or specified user
    github_user_name: ${{ github.repository_owner }}

    # list of files to generate.
    # one file per line. Each output can be customized with options as query string.
    #
    #  supported options:
    #  - palette:     A preset of color, one of [github, github-dark, github-light]
    #  - color_snake: Color of the snake
    #  - color_dots:  Coma separated list of dots color.
    #                 The
…
View on GitHub
It uses GitHub Actions to build and update a user's contribution graph, and then has a snake eat all your contributions. The output generates a gif file, that you can then show on your GitHub Profile README. I thought this was pretty cool, so I set about adding this to my profile.

Step 1. Setting up GitHub Actions
The first thing you want to ensure before you start this project, is that you have GitHub Actions setup. Head to your Profile and ensure the "Actions" tab is available. Everyone should now have this feature.

Actions Button

Next, head to Platane's Action (available on the Marketplace) and make a copy of the code. You'll need to add this snippet into your Actions file.

Step 2. Creating your GitHub Actions yaml file
This is definitely the part where I got stuck. When looking at the code, I wasn't sure exactly where to add the lines of code mentioned on Marketplace.

After looking at the way Platane had their Actions file setup, I was able to generate the code (with a little help from Bdougie of course).

I've added the full code snippet below and added plenty of comments to (hopefully make it easy to understand).

You can copy this code straight into a blank *.yml file. Make sure you create a new *.yml file under the following directory:

YOUR_GITHUB_USERNAME --> .github --> workflows --> FILE_NAME.yml

# GitHub Action for generating a contribution graph with a snake eating your contributions.

name: Generate Snake

# Controls when the action will run. This action runs every 6 hours.

on:
  schedule:
      # every 6 hours
    - cron: "0 */6 * * *"

# This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:

    # Checks repo under $GITHUB_WORKSHOP, so your job can access it
      - uses: actions/checkout@v2

    # Generates the snake  
      - uses: Platane/snk@master
        id: snake-gif
        with:
          github_user_name: mishmanners
          # these next 2 lines generate the files on a branch called "output". This keeps the main branch from cluttering up.
          gif_out_path: dist/github-contribution-grid-snake.gif
          svg_out_path: dist/github-contribution-grid-snake.svg

     # show the status of the build. Makes it easier for debugging (if there's any issues).
      - run: git status

      # Push the changes
      - name: Push changes
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: master
          force: true

      - uses: crazy-max/ghaction-github-pages@v2.1.3
        with:
          # the output branch we mentioned above
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
Step 3. Running GitHub Actions
Once you've added the code above and committed it, head to your Actions tab. Under "Workflows", you should see the "Generate Snake" Action you created above.

Workflow

Click "Run Workflow" and watch your workflow run. You can even expand your workflow and see what's happening in real time.

Running Actions

Once your workflow has finished running, you should have received a green ✅ "build" checkmark. If so, this means your Action is working nicely. If not, you'll have to go through the code and see where the errors are. The "build" status should give you some indication of where your errors lie. You can also compare it with the yaml file on my GitHub Profile README.

Build green

If you have the green "build" ✅ then you should be good to go. Head back to your repo's "Code" directory, and change your branch to "output". Here you'll find the two versions of your contribution graph with the snake eating it: a *.gif and a *.svg. The good thing about these files is the file is rewritten over itself every time the Action runs. Thus, your contribution graph will always be up to date.

CodeOutput

Step 4. Adding a contribution-eating snake to your profile
Now the final set is to add this to your profile. Grab the file location of your *.gif. It should be something like:

https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-contribution-grid-snake.gif

Add this to your profile by copying the file location onto a new line in your markdown file:

![snake gif](https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-contribution-grid-snake.gif)

Now you should have a really cool looking snake eating your contributions!

GIFSnakeEating
Hopefully this guide was helpful for you and gives you a good base to start building and adding more Actions on your profile. What have you been adding to your GitHub Profile README? Other there other cool Actions I should be looking at?

GitHub Like a Boss (23 Part Series)
1
GitHub Desktop for better repo organisation
2
GitHub README for easy to understand code
...
19 more parts...
22
How to automatically close your issues once you merge a PR
23
How to get more suggestions from GitHub Copilot
👋 Before you go

Do your career a favor. Join DEV. (The website you're on right now)

It takes one minute and is worth it for your career.

Get started

Top comments (44)
Subscribe
pic
Add to the discussion
 
 
kushaltanna24 profile image
KushalTanna24
•
Jun 3 '22

Work fine.! Here is mine - KushalTanna24


2
 likes
Like
Reply
 
 
msoftware profile image
Michael jentsch
•
Jul 9 '21

Great tutorial! Works for me.
Here's mine - github.com/msoftware


2
 likes
Like
Reply
 
 
gustavohgmartins profile image
Gustavo Martins
•
Sep 3 '21

Awsome! How did you change the background-color?


Like
Reply
 
 
mishmanners profile image
Michelle Duke 
•
Sep 3 '21

I didn't change the background colour. It's a .png/.svg image, meaning the background is transparent. It looks dark on mine because I have dark mode enabled on GitHub. You can enable it by clicking Settings --> Appearance --> choosing your mode.


1
 like
Like
Thread
 
gustavohgmartins profile image
Gustavo Martins
•
Sep 3 '21

Thank you! actually I was using the .gif version, so I switched to the .svg one and voilá


2
 likes
Like
Thread
 
mishmanners profile image
Michelle Duke 
•
Sep 3 '21

Awesome! Glad to be of help 😄


1
 like
Like
Reply
 
 
1seamy profile image
seamy
•
Apr 9 • Edited on Apr 9

Thanks Michelle Mannering for your (dev.to/mishmanners/how-to-enable-g...) topic.

If other users wish to utilize this, kindly modify this topic;

1-Use this (thanks Platane github.com/Platane) file;

github.com/1SeaMy/1SeaMy/blob/main...

2-Use this;

![snake gif](https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-contribution-grid-snake-dark.svg)

or this

![snake gif](https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-contribution-grid-snake.svg)


3
 likes
Like
Reply
 
 
platane profile image
Platane
•
Aug 21 • Edited on Aug 21

Hi, First of all thanks for the precise tutorial!

There were a few changes in the action (mostly to adapt to github api), I had to change some parameters and bump the version.

Unfortunately a lot of people use the edge version ( with the tag #master ). It's a bit of a mess but the result is that this version is deprecated and can no longer work without adding some modification from the user (adding a github token as param)

The recommended usage is now this declaration:
- uses: Platane/snk/svg-only@v3
  with:
    github_user_name: ${{ github.repository_owner }}
    outputs: |
      dist/github-snake.svg
Check the readme for details about the new options


1
 like
Like
Reply
 
 
l3on06 profile image
L3on06
•
Feb 17 '23

Hello everyone, before proceeding, please navigate to 'Settings -> Actions -> General -> Workflow Permissions' in your README.md file and select 'Read and Write' permissions. This is important because if you have other permissions selected, it may result in errors.


2
 likes
Like
Reply
 
 
unknow0074 profile image
Unknown
•
May 27

I specially created account to say thank you I almost wasted my 3 hours in wandering around to fix issue and you saved my life.** Thank you**


Like
Reply
 
 
baayah profile image
BAayah
•
Jan 11

Thank you so much! I tried to change in settings 'Contribution' to 'include my private contributions' but anyway my Readme profile doesn't show My Contributions. Could you please help me with this?
github.com/BAayah/BAayah


Like
Reply
 
 
jakon62508112 profile image
Jakob
•
Jan 21 '23 • Edited on Jan 21

Getting this error when I try to run workflow and after it fails:
Node.js 12 actions are deprecated. Please update the following actions to use Node.js 16: actions/checkout@v2. For more information see: https://github.blog/changelog/2022-09-22-github-actions-all-actions-will-begin-running-on-node16-instead-of-node12/.


1
 like
Like
Reply
 
 
shuvajitgeek profile image
Shuvajit
•
Feb 2 '23

go to setting -> action -> and check the workflow as read and write
(run build again) hopefully you will not get error


Like
Reply
 
 
ariafatah profile image
Ariafatah
•
Sep 18 '23

github.com/ariafatah0711/ariafatah...

Check my github and change this file because I tried the file above only as much as it appears if you want to use the full one I use. And don't forget to give stars😁


1
 like
Like
Reply
 
 
ariafatah profile image
Ariafatah
•
Sep 18 '23

If the action fails, you can go to repo settings, click action, then select general, and look at the bottom where it says read and write.


1
 like
Like
Reply
 
 
bpolaswar profile image
Bhumesh Polaswar
•
Oct 17 '21

Great worked for me. See github.com/bpolaswar
Thanks.


2
 likes
Like
Reply
 
 
hoangtien_2k3 profile image
Hoàng Anh Tiến
•
Jan 29 '23 • Edited on Jan 29

It does not work for me. Can someone help me?
github.com/hoangtien2k3qx1

Error:
actions/checkout@v2, platane/snk@master, ad-m/github-push-action@master, and crazy-max/ghaction-github-pages@v2.1.3 are not allowed to be used in hoangtien2k3qx1/hoangtien2k3qx1. Actions in this workflow must be: within a repository owned by hoangtien2k3qx1.


1
 like
Like
Reply
 
 
viveeeeeek profile image
VivekS.
•
Oct 3 '21

Awesome!


1
 like
Like
Reply
 
 
shasank27 profile image
Shasank Periwal
•
Aug 8 '21 • Edited on Aug 8

Great tutorial!
But can anyone help me, its not showing all my contributions
github.com/shasank27/shasank27


1
 like
Like
Reply
 
 
mishmanners profile image
Michelle Duke 
•
Sep 6 '21 • Edited on Sep 6

Hey Shasank. I can't see it on your profile, but to show all contributions, you need to make sure all contributions are turned on your profile. You can do this in your settings:

github.com/YOUR_PROFILE --> Settings --> Profile

Then scroll down to "Contributions" and check the box that says "Include private contributions on my profile".

Hope that helps.


1
 like
Like
Reply
 
 
hudsonpufferfish profile image
Hudson Nguyen
•
Jan 8 '23

I got error "The process '/usr/bin/git' failed with exit code 128". Even though I tried to generate a new personal access token, it didn't work. Anybody has any solution for this error?


1
 like
Like
Reply
 
 
1seamy profile image
seamy
•
Apr 9

Thanks :)


1
 like
Like
Reply
 
 
nirav97120 profile image
Nirav Prajapati
•
Dec 16 '22

Awesome My github profile


2
 likes
Like
Reply
View full discussion (44 comments)
Code of Conduct • Report abuse
profile
Warp
Promoted

Warp code image

Warp AI to the rescue.
Solve issues with a terminal that understands natural language. Try it today.

Try it today.

Read next
dvalin99 profile image
7 Open Source Projects You Should Know - Python Edition ✔️
Domenico Tenace - Aug 12

judith677 profile image
#38 — Group Columns of An Excel Table And Perform Aggregation
Judith-Excel-Sharing - Aug 2

jwilliamsr profile image
A Guide to Machine Learning System Design and Best Practices
Jesse Williams - Aug 12

baltasarq profile image
Creando un Tetris con JavaScript IV: canvas
Baltasar García Perez-Schofield - Jul 10


Michelle Duke
Follow
Developer Advocate | Hackathon Queen | International Speaker
Location
Australia
Education
The University of Melbourne
Work
Developer Advocate at GitHub
Joined
May 29, 2020
More from Michelle Duke
How to test websites: Using SIRV and Playwright for test driven development (TDD)
#javascript #webdev #programming #tutorial
Release Radar · July 2024: Major updates from the open source community
#github #community #news #developers
Release Radar · June 2024: Major updates from the open source community
#github #community #news #developers
profile
Heroku
Promoted

Heroku

Simplify your DevOps and maximize your time.
Since 2007, Heroku has been the go-to platform for developers as it monitors uptime, performance, and infrastructure concerns, allowing you to focus on writing code.

Learn More


# GitHub Action for generating a contribution graph with a snake eating your contributions.

name: Generate Snake

# Controls when the action will run. This action runs every 6 hours.

on:
  schedule:
      # every 6 hours
    - cron: "0 */6 * * *"

# This command allows us to run the Action automatically from the Actions tab.
  workflow_dispatch:

# The sequence of runs in this workflow:
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:

    # Checks repo under $GITHUB_WORKSHOP, so your job can access it
      - uses: actions/checkout@v2

    # Generates the snake  
      - uses: Platane/snk@master
        id: snake-gif
        with:
          github_user_name: mask-shakill
          # these next 2 lines generate the files on a branch called "output". This keeps the main branch from cluttering up.
          gif_out_path: dist/github-contribution-grid-snake.gif
          svg_out_path: dist/github-contribution-grid-snake.svg

     # show the status of the build. Makes it easier for debugging (if there's any issues).
      - run: git status

      # Push the changes
      - name: Push changes
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: master
          force: true

      - uses: crazy-max/ghaction-github-pages@v2.1.3
        with:
          # the output branch we mentioned above
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
Thank you to our Diamond Sponsor Neon for supporting our community.

DEV Community — A constructive and inclusive social network for software developers. With you every step of your journey.

Home
DEV++
Podcasts
Videos
Tags
DEV Help
Forem Shop
Advertise on DEV
DEV Challenges
DEV Showcase
About
Contact
Guides
Software comparisons
Code of Conduct
Privacy Policy
Terms of use
Built on Forem — the open source software that powers DEV and other inclusive communities.

Made with love and Ruby on Rails. DEV Community © 2016 - 2024.
























<h1 align="center">Hi 👋, Md. Al Shaharirar Kobir Shakil/h1>
<h3 align="center">A Software Developer who loves to Develop, Analyze and Innovate</h3>


 


<h2 align="center">Languages and Tools:</h3>
<div align="center">
  <img src="https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white&style=for-the-badge" height="33" alt="typescript logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white&style=for-the-badge" height="33" alt="python logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white&style=for-the-badge" height="33" alt="nodejs logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Next.js-000000?logo=nextdotjs&logoColor=white&style=for-the-badge" height="33" alt="nextjs logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/React-61DAFB?logo=react&logoColor=black&style=for-the-badge" height="33" alt="react logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black&style=for-the-badge" height="33" alt="javascript logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Tailwind CSS-06B6D4?logo=tailwindcss&logoColor=black&style=for-the-badge" height="33" alt="tailwindcss logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Express-000000?logo=express&logoColor=white&style=for-the-badge" height="33" alt="express logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Flask-000000?logo=flask&logoColor=white&style=for-the-badge" height="33" alt="flask logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white&style=for-the-badge" height="33" alt="docker logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Prisma-2D3748?logo=prisma&logoColor=white&style=for-the-badge" height="33" alt="prisma logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white&style=for-the-badge" height="33" alt="html5 logo"  />
  <img width="10" />
  <img src="https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black&style=for-the-badge" height="33" alt="linux logo"  />
</div>
