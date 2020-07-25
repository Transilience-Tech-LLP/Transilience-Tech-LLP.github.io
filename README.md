# A static informational website.

- The site uses jekyll to build.

## Idea

- Our website would mostly have static content to it. Therefore jekyll served from github will give a significant boost the site.
- Since github pages supports jekyll we should use jekyll as our preferred development platform.
- Jekyll is a html builder, it parses the markdown data and eits out html code, thus we need to do less for the site to be up and running.

## Layout.

- The site has pages on the root. 
- In case a page uses extension .md, it will be compiled to an html, but if we define layout in the page itself ,we need to use .html as an extension
- To add more pages, add a layout for that page if different from existing layouts. the layout go into _layouts folder.


## Posts

- The posts go into _posts folder.
- Posts musyt be md. they need to have front matter to be there in the posts for them to be parsed
- The posts may contain a youtube link
- 
