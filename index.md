### Welcome to GitHub Pages.
This automatic page generator is the easiest way to create beautiful pages for all of your projects. Author your page content here [using GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/), select a template crafted by a designer, and publish. After your page is generated, you can check out the new `gh-pages` branch locally. If you’re using GitHub Desktop, simply sync your repository and you’ll see the new branch.

### Designer Templates
We’ve crafted some handsome templates for you to use. Go ahead and click 'Continue to layouts' to browse through them. You can easily go back to edit your page before publishing. After publishing your page, you can revisit the page generator and switch to another theme. Your Page content will be preserved.

### Creating pages manually
If you prefer to not use the automatic generator, push a branch named `gh-pages` to your repository to create a page manually. In addition to supporting regular HTML content, GitHub Pages support Jekyll, a simple, blog aware static site generator. Jekyll makes it easy to create site-wide headers and footers without having to copy them across every page. It also offers intelligent blog support and other advanced templating features.

### Authors and Contributors
You can @mention a GitHub username to generate a link to their profile. The resulting `<a>` element will link to the contributor’s GitHub Profile. For example: In 2007, Chris Wanstrath (@defunkt), PJ Hyett (@pjhyett), and Tom Preston-Werner (@mojombo) founded GitHub.

### Support or Contact
Having trouble with Pages? Check out our [documentation](https://help.github.com/pages) or [contact support](https://github.com/contact) and we’ll help you sort it out.

<ul>
            {% for post in paginator.posts %}
              <li>
                <h2>
                  <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
                </h2>
                <div class="label">
                    <div class="label-card">
                        <i class="fa fa-calendar"></i>{{ post.date | date: "%F" }}
                    </div>
                    <div class="label-card">
                        {% if post.author %}<i class="fa fa-user"></i>{{ post.author }}
                        {% endif %}
                    </div>
                    <div class="label-card">
                        {% if page.meta %}<i class="fa fa-key"></i>{{ page.meta }}  {% endif %}
                    </div>

                    <div class="label-card">
                    {% include category.html %}
                    </div>

                    <div class="label-card">
                    {% include tag.html %}
                    </div>
                </div>
                <div class="excerpt">
                    {{post.excerpt}}
                </div>
                <div class="read-all">
                    <a  href="{{ post.url | prepend: site.baseurl }}"><i class="fa fa-newspaper-o"></i>Read All</a>
                </div>
                <hr>
              </li>
            {% endfor %}
        </ul>