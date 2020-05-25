# Yu's Blog

This blog intends to share ideas and share notes with others. Questions and doubts are welcome.

## Log of building the blog
- The first version of the blog is built following the guidance on the [Kresnik's blog](http://kresnik.wang/works/tech/2015/06/07/在github-pages网站下用jekyll制作博客教程.html), using the template [Flexible-Jekyll theme](http://jekyllthemes.org/themes/flexible-jekyll/) from [jekyllthemes](http://jekyllthemes.org). 
- The second version used a new template [Jekyll Theme Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy#jekyll-theme-chirpy), and was built on github.io page.
- The third version still used the Chirpy theme, but the updated version. This version is now built on github.io/project page.

## MathJax
- Enable MathJax by adding the following to the `\_include/head.html` file. There are some major changes from Mathjax 2 to 3. Now I am using Mathjax 3. Check [kramdown Syntax](https://kramdown.gettalong.org/syntax.html)for detailed instructions on math blocks in kramdown, which is used in this blog framework.
	```html
	<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
	```
- Inline math:
	```md
	This is inline math: $$x = 3$$, and $$y = 5$$.
	```
- Display math:
	```md
	$$
	x = y + 4
	$$
	```

## Table of contents
In order to have sidebar table of contents, the headings should start from heading 1 or 2, not 3. 

## Steps to push to Github
Since there is something wrong with ruby-gem on my mac, so I use Google Cloud to build this blog, and VS Code greatly helps me to edit remote files. After making modifications on the files, `git add` and `git commit`, then
```console
bash tools/init.sh
git push
```

## License
GNU General Public License v3.0