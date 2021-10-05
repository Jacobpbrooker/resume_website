---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
# ![]({{site.avatar}})
#<img class="avatar" src="https://goo.gl/khGCrk" alt="avatar" /> <meta charset="utf-8">
layout: home
Title: "Welcome!"
list_title: "Coding Projects"
---
<div>
    <h1><b>{{page.Title}}</b><br></h1>
    <hr>
</div>

~~~c++
#include stdio.h
#include stdlib.h

int main(void) {
    bool coop_search = true;

    if(coop_search)
        printf("Hello and welcome to my project showcase website!\n");
        printf("To learn more about various projects from my Github Repository 
                    check out any of my posts below\n");
        printf("To get to know me a little better, check out my \"About Me\" page\n");
        printf("If you want to get in contact with me you will find my email, 
                    LinkedIn, and GitHub links at the foot of the page\n");
        printf("Thank you for stopping by and I hope you enjoy!\n");
    }
    else{
        printf("Just enjoy the work!");
    }

    exit(EXIT_SUCCESS);
}
~~~
<br>
