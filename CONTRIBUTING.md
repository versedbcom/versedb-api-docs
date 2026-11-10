# Contributing

- Guides live in `guides/`, one Markdown file per topic. Each starts with YAML front matter:

  ```yaml
  ---
  title: Rate Limits
  description: One plain sentence, used as the page's meta description.
  order: 6
  ---
  ```

  `order` sets the reading order. Write plain CommonMark with GitHub tables; raw HTML is escaped when the page is rendered, so don't use it. Link to another guide by its file name, such as `[Acceptable Use](acceptable-use.md)`.
- `openapi.json` and `postman.json` are generated from the live API every night. Don't edit them; changes to them are overwritten.
- If an endpoint description, parameter or example is wrong, open an issue.
