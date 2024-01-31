# Ally's Blog
This blog is set up using Hexo, a static site generator.

## Getting Started
To run this blog locally, make sure you have Node.js and Hexo installed.

1. Clone this repository
2. Run `npm install` to install dependencies
3. Run `hexo server` to start the local development server
4. Visit http://localhost:4000/hexo-blog/ to see the blog

## Writing Posts
Posts are written in Markdown format and stored in the source/_posts directory.

To create a new post, run:
```
hexo new ${"Your Post name"}
```

This will generate a template Markdown file that you can fill with your content.

## Deploying

To deploy the site, run:
```
hexo generate
```
This will generate the static files in the public folder. Then run:
```
hexo deploy
```
This will deploy the site to GitHub Pages. The site is automatically rebuilt whenever you commit changes to the source folder.

## Tools Used
- Node.js - For running Hexo
- Hexo - Static site generator
- Markdown - For writing blog posts
- GitHub Pages - For hosting the site

## Theme

This blog's theme is fork from [hexo-theme-pure](https://github.com/renbaoshuo/hexo-theme-pure), it's really a good theme, thanks to the author [Baoshuo](https://github.com/renbaoshuo).

That's the basics of how this Hexo blog works. Let me know if you need any clarification or have additional questions!