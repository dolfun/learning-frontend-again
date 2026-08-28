# Progress tracker

Do check out my [GitHub](http://github.com/dolfun/) or my [ShaderToy](https://www.shadertoy.com/user/Dolfun) profile. \
[Resources page](resources.md)

## Day 11 (Aug 27)

Read about [`overflow` property](https://css-tricks.com/almanac/properties/o/overflow/), [A Complete CSS Flexbox Layout Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/),

- `overflow: visible | hidden | scroll | auto | inherit`:
  - `visible`: Default. Content is not clipped when it proceeds outside its box. Even though the content is visible outside of the box, that content does not affect the flow of the page.
  - `hidden`: Overflowing content will be hidden and inaccessible.
  - `scroll`: Overflowing content will be hidden and but accessible via scrolling.
  - `auto`: The scrollbars will only show up if there is content that actually breaks out of the element.
- Properties for flex container:
  - `display: flex`: enables flexbox.
  - `flex-direction: row | row-reverse | column | column-reverse`
  - `flex-wrap: nowrap | wrap | wrap-reverse`
  - `flex-flow: [flex-direction] [flex-wrap]`
  - `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right ... + safe | unsafe`
    - `justify-content` defines the alignment along the main axis.
    - `safe` keeps the overflowing content accessible on the readable/scrollable side by changing an overflow alignment like `center` into a `start` alignment.
    - `unsafe` strictly enforces your chosen alignment, which can push parts of the content completely off-screen into an unscrollable area.
    <!-- markdownlint-disable-next-line MD033 -->
    <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg" alt="justify-content illustration" width="50%"></div>
  - `align-items: stretch | flex-start | flex-end | center | baseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe`
    - `align-items` defines the default behavior for how flex items are laid out along the cross axis on the current line.
    - `flex-start`: Flex container's cross-axis start
    - `start`: Flex container's writing mode
    - `self-start`: Individual flex own writing mode
    <!-- markdownlint-disable-next-line MD033 -->
      <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/10/align-items.svg" alt="align-items illustration" width="50%"></div>
  - `align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch | start | end + ... safe | unsafe`
    - `align-content` aligns a flex container’s lines within when there is extra space in the cross-axis.
    - This property only takes effect on multi-line flexible containers, where `flex-wrap` is set to either `wrap` or `wrap-reverse`.
      <!-- markdownlint-disable-next-line MD033 -->
      <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/10/align-content.svg" alt="align-content illustration" width="50%"></div>
  - `gap`, `row-gap` and `column-gap`:
    - `gap: [row and column gap]`
    - `gap: [row gap] [column gap]`
- Properties for flex items:
  - `order`: It controls the order in which they appear in the flex container. \
    Default is zero. \
    Items with the same `order` revert to source order.
  - `flex-grow`: Default is 1. It dictates what amount of the available space inside the flex container the item should take up as a proportion.
  - `flex-shrink`: Similar to `flex-grow` but for the case of shrinking.
  - `flex-basis`: It sets the initial size of a flex item along the main axis before the remaining space is distributed.
  - `align-self`: This allows the default alignment (or the one specified by `align-items`) to be overridden for individual flex items.
  - `flex: [grow] [shrink] [basis]`:
    - `flex: initial` -> `flex: 0 1 auto`
    - `flex: auto` -> `flex 1 1 auto`
    - `flex: none` -> `flex 0 0 auto`
    - `flex: 1` -> `flex 1 1 0%`
    - `flex: 2 100px` -> `flex 2 1 100px`

## Day 10 (Aug 26)

Read about the [`display` property](https://css-tricks.com/almanac/properties/d/display/) and [media queries](https://css-tricks.com/a-complete-guide-to-css-media-queries/). \
Read the [An Interactive Guide to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/). \
Finished the [Flexbox Froggy](https://flexboxfroggy.com/) game.

- An `inline` element will accept `margin` and `padding` but it will only push other elements horizontally away, not vertically. It will ignore `height` and `width`.
- `inline-block` will respect `height` and `width`.
- Anatomy of a media query: ![Anatomy of a media query](https://i0.wp.com/css-tricks.com/wp-content/uploads/2020/09/media-query-anatomy.jpg)
- Flexbox Diagram:
  <!-- markdownlint-disable-next-line MD033 -->
  <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/11/00-basic-terminology.svg" alt="Flexbox Diagram" width="80%"></div>

## Day 9 (Aug 25)

Read about CSS: psuedo-elements, [`position` property](https://css-tricks.com/almanac/properties/p/position/) and [units](https://yurilee.hashnode.dev/css-units-are-confusing-af).

- Psuedo-elements:
  - `::before`: Adds something before the element's content.

    ```css
    .hello::before {
      content: "👋 ";
    }
    ```

  - `::after`: Adds something after the element's content.
  - `::first-letter`: Styles the first letter of text.
  - `::first-line`: Styles the first line of a paragraph.
  - `::selection`: Controls how text looks when the user highlights it.
- `!important` is a keyword flag used to force a specific style declaration to override any conflicting styles.
- `:is()` and `:where()` are CSS pseudo-class function that lets you group multiple selectors without repeating the common part. \
  For example:

  ```css
  h1:hover, h2:hover, h3:hover {
    color: red;
  }
  ```
  
  Can be written as:

  ```css
  :is(h1, h2, h3):hover {
    color: red;
  }
  ```

- `:is()` keeps the specificity of its most specific argument while `:where()` always has zero specificity.
- Units cheatsheet:
  ![CSS Units](https://yurilee.hashnode.dev/_next/image?url=https%3A%2F%2Fcdn.hashnode.com%2Fres%2Fhashnode%2Fimage%2Fupload%2Fv1626960364359%2FRITHUchJLk.png&w=3840&q=100)
- `position` property can take the following values:
  - `static`: Default. Element sticks to the normal page flow. `left`/`right`/`top`/`bottom`/`z-index` have no effect.
  - `relative`: Same as `static` but the positional properties move the element from the original position in that direction.
  - `absolute`: The element is removed from the flow of the document and other elements will behave as if it’s not even there. \
  The positioning origin is the padding edge of its nearest positioned ancestor (an ancestor element whose position is anything other than `static`).
  - `fixed`: The element is fixed to the viewport.
  - `sticky`: The element is treated like a `relative` value until the scroll location of the viewport reaches a specified threshold, at which point the element takes a `fixed` position where it is told to stick.
  - `inherit`: It inherits the positioning value from its parent.

## Day 8 (Aug 24)

Finished the [CSS Diner](https://flukeout.github.io/) minigame.\
Read about CSS: psuedo-classes and flexbox. \
Re-read CSS layout, box model and sticky.

- Psuedo-classes:
  - `:first-child`: Select a first child element inside of another element.
  - `:only-child`: Select an element that are the only element inside of another one.
  - `:last-child`: Select the last element inside of another element.
  - `:nth-child(n)`: Select an element by its order in another element.
  - `:nth-last-child(n)`: Select an element by its order in another element, counting from the back.
  - `:first-of-type`: Select the first element of a specific type.
  - `:nth-of-type(n)`: Selects a specific element based on its type and order in another element - or even or odd instances of that element.
  - `:nth-of-type(an+b)`: The nth-of-type formula selects every ath element, starting the count at a specific instance (bth) of that element.
  - `:only-of-type`: Select elements that are the only ones of their type within of their parent element
  - `:last-of-type`: Select the last element of a specific type.
  - `:empty`: Select elements that don't have children.
- **Negation Pseudo-class**: `:not(X)`

- Flexbox is enabled with `display: flex`
- `flex-direction: row|column` determines the primary and cross axis.
- We can change how children are distributed along the primary axis using the `justify-content` property and for the cross axis we use the `align-items` property.
- `justify-content: flex-start|center|flex-end|space-around|space-between|space-evenly`
- `align-items: flex-start|center|flex-end|stretch|baseline`
- `align-self` is applied to the child element, not the container. It allows us to change the alignment of a specific child along the cross axis.
- `align-self` has all the same values as `align-items`.
- Definitions:
  - `justify` — to position something along the primary axis.
  - `align` — to position something along the cross axis.
  - `content` — a group of “stuff” that can be distributed.
  - `items` — single items that can be positioned individually.
- Box model illustration:
  <!-- markdownlint-disable-next-line MD033 -->
  <div style="text-align: center;"><img src="https://web.dev/static/learn/css/box-model/image/a-diagram-showing-four-m-af72960a9e79a.svg" alt="Box model illustration" width="80%"></div>
- `box-sizing: content-box` is the default, width and height apply only to the content. \
  In `box-sizing: border-box` width and height include the content, padding, and border.
  
- To set the box sizing model to border-box for every element and every pseudo-element:
  
  ```css
  *, *::before, *::after {
    box-sizing: border-box;
  }```
- To make an element sticky, you must pair `position: sticky`; with at least one threshold inset property, such as `top`, `bottom`, `left`, or `right`.

## Day 7 (Aug 21)

Read about HTML forms and CSS Selectors.

- To explicitly associate a form control with a `<label>`, include the `for` attribute on the `<label>`, the value being the `id` of the form control it is associated with:
  
  ```html
  <form method="GET">
    <label for="student">Pick a student:</label>
    <select name="student" id="student">
      <option value="hoover">Hoover Sukhdeep</option>
      <option>Blendan Smooth</option>
      <option value="toasty">Toasty McToastface</option>
    </select>
    <input type="submit" value="Submit Form">
  </form>
  ```

- To provide implicit labels, include the form control between the opening and closing `<label>` tags.

- While individual input, select, and text areas are labeled with `<label>`, groups of form controls are labeled by the contents of the `<legend>` of the `<fieldset>` that groups them.
- The `method` attribute on the `<form>` tag defines the HTTP protocol of the request.
- With `GET`, the form data is sent as a parameter string of `name=value` pairs, appended to the action's URL.
- With `POST`, the data is appended to the body of the HTTP request.
- Radio button group:
  
  ```html
  <input type="radio" name="student" value="blendan"> Blendan
  <input type="radio" name="student" value="hoover"> Hoover
  <input type="radio" name="student" value="toasty"> Toasty
  ```

  The `name` attribute should be unique to the group.

- The file input type `<input type="file">` enables uploading files via forms.
- One cannot start a class (or an ID) with a number.
- CSS Selectors:
  - Universal selector - `*`
  - Type selector - `section`
  - Class selector - `.my-class`
  - ID selector - `#rad`
  - Attribute selector - `[data-type]`, `[data-type='primary']`
  - Compound selectors - `a.my-class`
- You can use case-sensitive attribute selectors by adding an `s` operator to your attribute selector: `[data-type='primary' s]`
- Attribute matcing:
  - `[href*='example.com']`: A href that contains "example.com"
  - `[href^='https']`: A href that starts with https
  - `[href$='.com']`: A href that ends with .com
- Combinators:
  - Descendant (`div p`): It targets any `p` inside the `div`.
  - Child (`div > p`): `<p>` must sit exactly one level below the `div`.
  - Subsequent sibling (`h1 ~ p`): Targets all `p` elements that follow the `h1`.
  - Next sibling (`h1 + p`): Targets only the very next sibling.
  - Comma Combinator (`h1, p`): Targets both `h1` and `p`.
- Examples:
  - `.top * + *`: Any element inside `.top` that immediately follows another element.
  - `.top > * + *::before`: The `::before` of any direct child of `.top` that immediately follows another direct child.
- [A tool that translates CSS selectors into plain-english explainers](https://kittygiraudel.github.io/selectors-explained/?)

## Day 6 (Aug 20)

Finished the remote section of [learngitbranching.js.org](https://learngitbranching.js.org/) tutorial. \
Read about HTML: `<image>` and `<table>`.

- `srcset` attribute:

  ```html
  <img src="images/eve.png" alt="Eve"
    srcset="images/eve.png 400w, images/eve-xl.jpg 800w"
    sizes="(max-width: 800px) 400px, 800px" />
  ```

- `<picture>` and `<source>` tags (!?):

  ```html
  <picture>
    <source
      srcset="images/eve.png 400w, images/eve-xl.jpg 800w"
      sizes="(max-width: 800px) 400px, 800px">
    <img src="images/eve.png" alt="Eve">
  </picture>
  ```

- At a minimum, each foreground image should include `src` and `alt` attributes.
- Lazy loading: `<img src="switch.svg" alt="light switch" loading="lazy" />`
- The preferred method of naming a table is the semantic element, `<caption>`.
- Table sectioning:
  
  ```html
  <table>
    <caption></caption>
    <thead></thead>
    <tbody></tbody>
    <tfoot></tfoot>
  </table>
  ```

- To join multiple cells into a single cell, use `colspan` and `rowspan` attributes.
- Only use a table for data.

## Day 5 (Aug 19)

Read about HTML: lists and navigation (table of content and page breadcrumbs). \
Finished the main section of [learngitbranching.js.org](https://learngitbranching.js.org/) tutorial.

- `menu` tag acts as a semantic alternative to the `ul` tag.
- Description list, i.e., `dl` tag:

  ```html
  <dl>
    <dt>Description Term 1</dt>
    <dd>Description Detail 1</dd>
    <dt>Description Term 2</dt>
    <dd>Description Detail 2</dd>
  </dl>
  ```

- "Skip to content" link:
  
  ```html
  <a href="#main" class="skip-link button">Skip to content</a>
  <main id="main">
    Content
  </main>
  ```

- `aria-label` and `aria-labelledby` attributes define the accessible name of an element.
- The current page could be identified with the `aria-current="page"` attribute.

## Day 4 (Aug 18)

Read about HTML document structure, semantic tags, headings and links.

- HTML template:

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="utf-8" />
      <title>Title</title>
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    </head>
    <body>
      <!-- Body -->
    </body>
  </html>
  ```

- Favicon: `<link rel="icon" type="image/png" href="/images/favicon.png">`
- [<script src="..." async/defer>](https://javascript.info/script-async-defer)
- Some Semantic HTML Tags: `header`, `nav`, `main`, `section`, `article`, `aside` and `footer`.

  ```html
  <body>
  <header>Header</header>
  <nav>Nav</nav>
  <main>
    <article>First post</article>
    <article>Second post</article>
  </main>
  <aside>Aside</aside>
  <footer>Footer</footer>
  </body>
  ```

- [`tabindex`](https://web.dev/learn/html/attributes#tabindex) and [`contenteditable`](https://web.dev/learn/html/attributes#contenteditable) attributes

- `taget="_blank"` attribute on `a` tag open link in a new tab.

## Day 3 (Aug 17)

Read about Box model, revised git and started reading about HTML.

## Day 2 (Aug 13)

Read about `git tag`, `git log`, `git branch`, `git merge`, `git reset`, `git revert`, `git reflog` and `git rebase`.

### `git tag`

- `git tag <tagname> <commit_hash>`: Lightweight tags.
- `git tag -a <tagname>`: Annotated tags store extra meta data such as: the tagger name, email, and date.
- `git tag -l <wildcard>`: List tags with wildcard
- In the event that you must update an existing tag, the `-f FORCE` option must be used.
- `git push --tags`: 👍

### `git checkout`

- `git checkout -b ＜new-branch＞ ＜existing-branch＞`

### `git revert`

- It will create a new commit with the inverse of the last commit.

## Day 1 (Aug 12)

Read about `git init`, `git clone`, `git config`, `git alias`, `git add`, `git commit`, `.gitignore`, `git fetch`, `git pull` and `git push`.

### `git init`

- `git init --bare <directory>`: Initialize an empty Git repository, but omit the working directory.
- `git init <directory> --template=<template directory>`: Initialize a new Git repository and copy files from the  `＜template_directory＞` into the repository.
- `git init --quiet`
- `git init --separate-git-dir=<dir>`

### `git clone`

- `git clone <repo> <directory>`
- `git clone <repo> --branch <tag>`
- `git clone --depth 1`: shallow clone
- `git clone --bare` and `git clone --mirror` (?)

### `git config`

- `git config --[local/global/system] user.[name/email] <value>`

### `git add`

- `git add -p`: Begin an interactive staging session that lets you choose portions of a file to add to the next commit.

### `git commit`

- `git commit -a`: Commit a snapshot of all changes in the working directory. This only includes modifications to tracked files.

### `git stash`

- `git stash` and `git stash [pop/apply]`
- `git stash` will not stash new files in your working copy that have not yet been staged and files that have been ignored.
- `git stash save "message"`
- `git stash list`
- `git stash pop stash@{2}`
- `git stash drop stash@{1}` and `git stash clear`

### `.gitignore`

- [Git Ignore Patterns](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)
- **Ignoring a previously committed file**:
    1. `echo debug.log >> .gitignore`
    2. `git rm --cached debug.log`
    3. `git commit -m "Start ignoring debug.log"`
- **Committing an ignored file**: `git add -f debug.log`
- **Debugging `.gitignore` files**: `git check-ignore -v debug.log`
  
  The output shows:
  `<file containing the pattern>:<line number of the pattern>:<pattern>  <file name>`

### `git fetch`

- `git fetch <remote>`: Fetch all of the branches from the repository. This also downloads all of the required commits and files from the other repository.
- `git fetch <remote> <branch>`: Only fetch the specified branch.
- `git fetch --all`: Fetches all registered remotes and their branches.
- `git fetch --dry-run`: It will output examples of actions it will take during the fetch but not apply them.

### `git pull`

- `git pull` = `git fetch` + `git merge`
- `git pull --rebase`
- `git pull --no-commit`: Unlike `git fetch`, it modifies the local working branch, but does not create an automatic commit.

### `git push`

- `git push <remote> --force`: 😱
- `git push <remote> --tags`: This flag sends all of your local tags to the remote repository as tags are not automatically pushed.
- **Deleting a remote branch or tag**: `git branch -D branch_name` followed by `git push origin :branch_name`
