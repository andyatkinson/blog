## Hello!

This is the source for my website, blog, and portfolio at [andyatkinson.com](https://andyatkinson.com) built with Jekyll and hosted on Github Pages.

#### Theme bugs and issues

The `include` for the social link icons does not work on Heroku but worked locally. The `icons` folder is nested one layer deeper and it may just be that the relative filepath is not working.
This was worked around for now by inlining the contents of the `include`.

Multi-word tags had a whitespace character after the hyphen. Removed that so URLs worked.

`site.baseurl` did not have a leading slash in `_layouts/post.html` and did elsewhere, so this was breaking links. For now I manually inserted the leading slash in that file.

#### More Resources

[Setting up Namecheap DNS with Github Pages](https://www.namecheap.com/support/knowledgebase/article.aspx/9645/2208/how-do-i-link-my-domain-to-github-pages)

[Setting up Github Pages Custom Domains](https://github.blog/2018-05-01-github-pages-custom-domains-https/)


### Development

    bundle exec jekyll serve --incremental

I occasionally `rm -rf _site` to remove the generated site completely. Changing `config.yml` requires restarting the development server.
