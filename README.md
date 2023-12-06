# John Evelyn's Blog

This project is in beta, under active development. Currently only the archive is fucntional, no feeds or daily publishing works.

# Blog Technical Structure

TL;DR: You can see all the historical dairy entries at "/archive/". The blog "/diary/" will publish them day-by-day as they are published, as if he was writing today.

A Jekyll collection of individually dated entries scrapped from the original dairy data source are permalinks in the archive.

The current blog run (or "reading" of the diary in live published blog posts), maps the original 17th century dates to modern publishing dates. These are pregenerated each blog run, waiting in the standard Jekyll `_posts` directory for Jekyll to publish them as their modern date arrives (jekyll builds at least once each day).

The permalink for each modern dated blog post has it's modern published date (initial filename part) removed from the URI, and uses the "slug" frontmatter, which is the original 17th century date. The "title" front matter is also set to the original 17th century date to avoid a generic post title (the second part fo the filename), this is a known issues/limitation of Jekyll.

`_posts` is treated as calendar scheduling system for the current blog run, regenerated with modern dates at the end of each blog run by a special utility. 

The actual post's content is imported from the archive collection using the modern post frontmatter slug, which maps to the collection item slug also.

# John Evelyn Diary Source

The original documents are from The Gutenberg Project books [41218](https://www.gutenberg.org/ebooks/41218) and [42081](https://www.gutenberg.org/ebooks/42081), see more on the about page.

HTML source files in ZIP archives, are in the `_source-data/` directory (although these will not be parsed by Jekyll directly). 

The archive posts are build by scraped/parsing the source data with a custom cli utility script, written in PHP (hopefully this will be rewritten to a more appropriate language at some point).

Another cli utility script is then used to generate the current blog run `_post` files (which only contain frontmatter "slug" and "title").


## Parsing "The Project Gutenberg eBook of The Diary of John Evelyn" HTML

The idea is to rip out the "posts" from the source material, with minimal manual effort and minimal metadata/yaml needed in each post. e.g. no title or layout frontmatter, this is handled by jekyll defaults.

Using SublimeText 4 find RegEx (PCRE2)

`(\d{1,2}.{1,2})[\s]+(January|February|March|April|May|June|July|August|September|October|November|December)[\s,]+(\d{4})`

find the bulk

`<p>((\d{1,2}.{1,2})[\s]+(January|February|March|April|May|June|July|August|September|October|November|December)[\s,]+(\d{4})). ` (note the trailing space)

replace with `---\nsource_date: $2 $3 $4\n---\n<p>`


# Site Theme

I settled on the [Hitchens](https://github.com/patdryburgh/hitchens) Jekyll theme, with only the masthead and brand colors are overridden form the themes default.

The following other themes were also considered.

- https://github.com/poole/poole
- https://github.com/poole/lanyon
- https://github.com/ronv/sidey


