# Notes

## Links

- Challenge URL: [https://www.frontendmentor.io/challenges/recipe-page-KiTsR8QQKm](https://www.frontendmentor.io/challenges/recipe-page-KiTsR8QQKm)
- Live Site URL: [https://finkusuma-dev.github.io/fem-recipe-page](https://finkusuma-dev.github.io/fem-recipe-page)

## HTML Implementation

- Applied mobile design.
- Wrapped the solution inside article, as it contains information that can be distributed independently. [^1]
- TODO: Change the `table` contains the nutrition list with `dl` element.

## HTML Issues

### `<img>` alternate text

I added an alternate text to the `img`, but on [MDN Image Guide](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_images#alternative_text), it mentions `alt` can be empty if the body adequately describes the image. Currently, I'm unsure if the image is sufficiently described by this text on the paragraph: "This classic omelette combines beaten eggs cooked to perfection, optionally filled with your choice of cheese, vegetables, or meats."

### Each `h2` and its following content is wrapped inside `section`

I'm not sure if it's always better to wrap `h2` and its following content inside `section`.

### `<header>` inside `<main>`

Currently, `h1` and `p` elements are directly inside `article`. I asked _Chrome AI Assistant_ on the `article` element if it's better to wrap the `h1` and `p` with the `header`, and the response was that it's a good practice but not mandatory. It could enhance the semantic structure and provide a clear container for introductory content. But having only two elements `h1` and `p`, adding `header` might be considered unnecessary complexity.

`header` inside `main` is an example on [Webdev Semantic HTML](https://web.dev/learn/html/semantic-html)

### Use `ul` & `ol` or `dl`

The list items within the preparation time and instructions sections, contain a strong element with text and a colon. I'm not sure if it's better use `dl` element with `dt` and `dd` instead.

## CSS Issues

### Section styling

Preparation section is a sibling of other sections. This make the CSS styling of other sections a bit complex:

```css
/* Start from 3nd section */
section:nth-of-type(1n + 3) {
  padding-top: 32px;
}
/* Start from 2nd section, and not the last section*/
section:nth-of-type(1n + 2):not(:last-of-type) {
  padding-bottom: 32px;
  border-bottom: 1px solid var(--color-Stone-150);
}
```

If `header`, `p`, and preparation `section` is put inside `div`, styling other sections can use `:not(:first-of-type)` and `:not(:last-of-type)`.

## Others

- Screen readers: orca (linux), NVDA, Jaws (windows), talkback (android). Currently, using orca and talkback to test the accessibility of the page.

## Resources

- https://www.w3.org/WAI/ARIA/apg/
- https://www.w3.org/WAI/ARIA/apg/patterns/landmarks/examples/general-principles.html
- https://web.dev/learn/html/semantic-html?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fhtml%2F%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fhtml%2Fsemantic-html

---

[^1]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article.
