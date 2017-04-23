---
layout: post
title: Easy New Post Jekyll command
date: 2017-04-23 13:47:28
categories: linux terminal
---

I love the terminal. And I love automatization. And I love forgetting about details.
For those of you that don't know, [Jekyll](https://jekyllrb.com/) is a very nice static site generator that is integrated with Github pages. It is what this blog uses to run.

The problem is creating a post involves going to a specific folder on your sistem, creating a new text file, writing a
specific header on the file, then saving this file, then adding, commiting and pushing to github. *SO COMPLICATED*.

So here is a simple ZSH function (should work in BASH too, I think) that does most of the work for you. **Keep in mind you
need to edit line 10** with your specific local Github page path. Also, it uses your $EDITOR to edit the file, but you
can customize this easily on line 16.

{%highlight bash %}
post() { 
    shortdate=$(date "+%Y-%m-%d")
    date=$(date "+%Y-%m-%d %H:%M:%S")
    title=$1
    title_mod=${1// /-}
    title_mod=${title_mod//,/}
    categories=${2//,/ }
    post_path="$HOME/blogcito/_posts/$shortdate-$title_mod.md" 
    if [[ ! -f $post_path ]]; then
        string="---\nlayout: post\ntitle: $title\ndate: $date\ncategories: $categories\n---"
        echo "$string" >> "$post_path"
    fi

    $EDITOR $post_path

    printf "Upload post? [N/y]: "
    read ans
    if [[ "$ans" == "y" ]]; then
        git add $post_path
        git commit -m "created post $tile"
        git push origin master
    fi
}
{% endhighlight %}

Usage:
```
post "your post name" "comma or space separated tags"
```

You will be asked if you want to push it to Github inmediatly after quitting your editor.

