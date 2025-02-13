# Notes

## Links

- Challenge URL: [https://www.frontendmentor.io/challenges/recipe-page-KiTsR8QQKm](https://www.frontendmentor.io/challenges/recipe-page-KiTsR8QQKm)
- Live Site URL: [https://finkusuma-dev.github.io/fem-recipe-page](https://finkusuma-dev.github.io/fem-recipe-page)

## HTML Implementations

- Applied mobile design (not yet applied the rem unit).
- Wrapped the solution inside article, as it contains information that can be distributed independently. [^1]
- Put the nutrition list inside a `table` element.

## HTML Issues

### `<img>` alternate text

I added an alternate text to the `img`, but on [MDN Image Guide](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_images#alternative_text), it mentions `alt` can be empty if the body adequately describes the image. Currently, I'm unsure if the image is sufficiently described by this text on the paragraph: "This classic omelette combines beaten eggs cooked to perfection, optionally filled with your choice of cheese, vegetables, or meats."

### Each `h2` and its following content is wrapped inside `section`

I'm not sure if it's a best practice to always wrap `h2` and its following content inside `section`, and also in which cases the section is not needed.

### `<header>` inside `<main>`

Currently, `h1` and `p` elements are directly inside `article`. I asked _Chrome AI Assistant_ on the `article` element if it's better to wrap the `h1` and `p` with the `header`, and the response was that it's a good practice but not mandatory. It could enhance the semantic structure and provide a clear container for introductory content. But having only two elements `h1` and `p`, adding `header` might be considered unnecessary complexity.

The `header` inside `main` is an example in [WebDev Semantic HTML](https://web.dev/learn/html/semantic-html).

### Use `ul` & `ol` or `dl`

The list items within the instructions sections, contain a strong element with text and a colon. Is there any chance of using `dl` element for this?

## CSS Implementations

- `img` element (mobile design): To make the `img` element full width, use negative margin and increase the width to extend through the inline paddings.
- list-item element (margin & padding): Before setting the margin and padding of the list-item according to Figma, first reset the margin & padding using:

  ```css
  * {
    margin: 0;
    padding: 0;
  }
  ```

  Then set the margin to align the marker with the text above it.

  ```css
  ul li {
    margin-left: 15px;
  }

  ol li {
    margin-left: 16px;
  }
  ```

  <img src="./_docs/li_align.jpg" width="300">

  And then set the margin and padding accordingly:

  ```css
  ul li {
    margin-left: calc(15px + 8px);
    padding-left: 16px;
  }

  ol li {
    margin-left: calc(16px + 8px);
    padding-left: 16px;
  }
  ```

  <img src="./_docs/li_apply_margin_padding.jpg" width="300">

- Make the list-item marker stretch along the list item height.

  After trial and error, this is what I came up with. I removed the list-style using `list-style: none`. Then created a new bullet (circle shape) using `li::before` pseudo-element. I positioned it vertically center using `position:absolute; top:50%; transform: translateY(-50%);`. It worked, but there was a problem, screenreaders didn't announce the bullet character.

  Then I removed the circle shape and used `content: '\2020'` to add the bullet character. The screenreader did announce it, but it was really difficult to precisely center the character vertically.

  My final solution is adding the circle shape again, but then hide the bullet character using `color: transparent`.

  ```css
  ul {
    list-style: none;
  }

  li {
    padding-left: 40px;
    position: relative;
  }

  li::before {
    /* Visual circle */
    width: 4px;
    height: 4px;
    border-radius: 4px;
    background-color: var(--color-Rose-800);

    /* Visual circle positioning, stretch along `li` height */
    top: 50%;
    left: 8px;
    transform: translateY(-50%);
    position: absolute;

    /* Visually hidden circle character so screenreader will announce: "bullet" */
    content: '\2022';
    color: transparent;
  }
  ```

- Nutrition list: The table had addition spaces somewhere that made overall height was more than the total height of the rows. This caused by default `border-collapse` property is `separate`, which separate the border between cells. To fix this I set `border-collapse` to `collapse`.

  ```css
  table {
    border-collapse: collapse;
  }
  ```

  There was also issue where `th` (1st column) and `td` (2nd column) width are not equal. When the table occupies the parent's width, the column's width distribution is affected by the basis width each of the column. And each of the column's width depends on the most wide cell in that column, which is impacted by the cell content.

  To make both columns equal, I set the width to `50%`.

  ```css
  th,
  td {
    width: 50%;
  }
  ```

## CSS Issues

### Section styling

Preparation section is the first sibling of other sections, which makes the CSS styling of other sections a bit more complex:

```css
/* Start from 3th section */
section:nth-of-type(1n + 3) {
  padding-top: 32px;
}
/* Start from 2nd section, and doesn't include the last section*/
section:nth-of-type(1n + 2):not(:last-of-type) {
  padding-bottom: 32px;
  border-bottom: 1px solid var(--color-Stone-150);
}
```

If the preparation `section` or the `header`, `p`, and preparation `section` are put inside `div`, styling other sections can be more simple with `section:not(:first-of-type)` and `section:not(:last-of-type)`.

## Others

- Screen readers: orca (linux), NVDA, Jaws (windows), talkback (android). Currently, using orca and talkback to test the accessibility of the page.

## Resources

- https://www.w3.org/WAI/ARIA/apg/
- https://www.w3.org/WAI/ARIA/apg/patterns/landmarks/examples/general-principles.html
- https://web.dev/learn/html/semantic-html?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fhtml%2F%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fhtml%2Fsemantic-html
- https://discord.com/channels/824970620529279006/1339214865243312128/1339227042784481290 - Grace Snow's feedback on discord about the same challenge.
- https://stackoverflow.com/questions/8900571/two-column-table-or-dl - Simple guide to choose whether to use two columns table or description list.
- https://www.w3.org/WAI/tutorials/tables/, https://www.w3.org/WAI/EO/Drafts/tutorials/tables/scope/ - W3C tutorial on scope of headers.
- https://css-tricks.com/everything-you-need-to-know-about-the-gap-after-the-list-marker/ - Unicode characters that can be used as a custom list marker.

---

[^1]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article.
