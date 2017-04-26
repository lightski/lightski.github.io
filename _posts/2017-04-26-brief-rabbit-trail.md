---
layout: post
title: A Brief Rabbit Trail
---

Due to time-constraints, I find myself unable to write a full hacking post today. So instead, here's my jekyll setup and workflow.

This site is currently hosted on [github pages](https://pages.github.com/), a free static hosting service for github users. The content is built using [jekyll](https://jekyllrb.com/). Jekyll takes markdown files as input, transforms them to html, and finally adds silliness such as comments and theming. 

My daily workflow is as follows:
1. switch to my blog's directory

    ```shell
    cd ~/my/blog/dir/
    ```
2. ask git to use the 'wip' branch (gotta keep 'master' clean)

    ```shell
    git checkout wip
    ```
3. cd to the \_posts directory

    ```shell
    cd _posts
    ```
4. copy an old post as basis for the next one

    ```shell
    cp 2017-04-24-first-post-1.md 2017-04-26-new-post.md
    ```
5. open new post with my favorite editor

    ```shell
    vim 2017-04-26-new-post.md
    ```
6. write post content (take notes and read)
7. open another terminal and build the site locally to test it

    ```shell
    cd ~/my/blog/dir/
    bundle exec jekyll serve
    ```
8. view the site content in a browser (http://localhost:4000/) to make sure I formatted the markdown correctly. Jekyll automatically rebuilds the site as I make changes.
9. when satisfied, add the new post to git. Then commit the change and merge it to the master branch.

    ```shell
    git add 2017-04-26-new-post.md
    git commit -m "Adds new post"
    git checkout master
    git merge wip
    ```
8. now that the content is complete, all that's left is to push it up to github. Github takes care of refreshing my site's content and making it available.

    ```shell
    git push origin master
    ```

This setup is nice for a variety of reasons:
1. It's a workflow similar to coding, which I've had some practice on. 
2. I can leverage familiar tools such as git and vim.
2. After 3 hours of initial setup, I don't have to worry about the theming any more.
3. Github takes care of building and hosting the site.

In short, I am highly satisfied with the jekyll workflow. It has made writing and publishing incredibly convenient for me. I can focus on the content rather than worrying about hosting, provisioning, and theming. Thanks github pages + jekyll! 

Tomorrow should be a return to form with the hacking book notes.
    
More to come.
