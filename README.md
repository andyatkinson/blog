## Hello!

This is the source for my website, blog, and portfolio at [andyatkinson.com](http://andyatkinson.com).

### July 2019 Updated Design and Content

Removed all puma related things for Heroku, now using the static site build pack.

#### Credits

 * [Royce Theme](https://jekyllthemes.io/theme/royce-blog-jekyll-theme)
 * [Heroku](https://heroku.com/)
 * [favicon.io](https://favicon.io/)
 * [Jekyll on Heroku instructions](https://blog.heroku.com/jekyll-on-heroku)


#### Bugs and known issues:

Insecure content warning on Heroku. Fix TBD.

The `include` for the social link icons does not work on Heroku but worked locally. The `icons` folder is nested one layer deeper and it may just be that the relative filepath is not working.
This was worked around for now by inlining the contents of the `include`.

Multi-word tags had a whitespace character after the hyphen. Removed that so URLs worked.

`site.baseurl` did not have a leading slash in `_layouts/post.html` and did elsewhere, so this was breaking links. For now I manually inserted the leading slash in that file.


### Run Jekyll Locally

    bundle exec jekyll serve --incremental

Note, that I occasionally have to `rm -rf _site` to remove the generated file cache. Changing the `config.yml` file requires restarting the development server.

