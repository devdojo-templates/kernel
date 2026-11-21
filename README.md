# Kernel

<img src="./thumbnail.png" style="width:100%; height:auto" />

The Kernel template for DevDojo: a personal site reduced to its index, one
narrow column of warm paper where every piece of writing and every project is
a row of type, a hairline leader and a date. Pages: Home, Writing (with a page
per piece), Projects (with a page per project), About and Now.

It is written in the HTML syntax of
[DevDojo Framework](https://github.com/thedevdojo/framework).

## What is in it

```
public/              served as it is: images, js, favicon.svg, robots.txt
src/
  pages/             one file for each page
    writing/[writings.slug].html   one page for each piece of writing
    projects/[projects.slug].html  one page for each project
  components/
    layouts/main.html              the page frame: head, nav, footer
    sections/                      the sections pages are made of
    nav.html, footer.html          the nav and the footer
  data/
    site.json                      the nav, the footer, the elsewhere links
    collections/*.json             writings, projects and background
  css/site.css       the theme: colours, type, leader rows and motion
  design.md          the design notes
template.json        how DevDojo lists the template
thumbnail.png        the picture DevDojo shows for it
```

A page is a list of sections:

```html
<Layout src="main.html" title="About" current="/about">
    <SectionsPageIntro heading="About" />
    <SectionsBackground heading="The short version" />
    <SectionsLinkGroup :links="site.elsewhere_links" heading="Elsewhere" />
</Layout>
```

A section is a file in `src/components/sections/`. It names what it takes in
`<Props />`, and the `.yml` beside it says how DevDojo's editor shows those
fields:

```html
<Props :links="[]" heading="Elsewhere" note="" />
<section>
    <h2>{heading}</h2>
    <ul role="list">
        <Foreach links="link">
            <li><a href="{link.url}">{link.text}</a></li>
        </Foreach>
    </ul>
    <If condition="note != ''">
        <p>{note}</p>
    </If>
</section>
```

## Running it

With the `devdojo` command from DevDojo Framework:

```bash
devdojo serve
```

serves the site at `http://localhost:8000` and reloads the page as you edit.

```bash
devdojo lint .
```

checks every page and prints anything that does not compile.
