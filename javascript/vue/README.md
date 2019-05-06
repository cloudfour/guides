# Vue Guide

This styleguide is a work-in-progress, documenting how Cloud Four prefers to write Vue. As we continue to expand it, please refer to these guides for additional best practices:

* [Official Vue Style Guide](https://vuejs.org/v2/style-guide/)
* [Deverus Vue Style Guide](https://gist.github.com/brianboyko/91fdfb492071e743e389d84eee002342)
    * [Erik reviews the Deverus Style Guide](https://www.youtube.com/watch?v=38XnZ3EJqYQ)

## Destructuring in Templates

Try to avoid destructuring in HTML templates, to make it obvious where a particular variable is coming from. Since HTML templates have access to props and local variables in `v-for` loops, clarity is favored over brevity in this case.

**Bad**

Notice that in this example with nested `v-for` loops, destructuring makes it unclear where certain variables are coming from, and some repeated variables like `title` need to be remapped.

```vue
<section v-for="{ title, id, subcategories, items } in FAQs" :key="id">
  <h2>{{ title }}</h2>

  <section
    v-for="{ title: subtitle, items: subItems, subcategoryId } in subcategories"
    :key="subcategoryId"
  >
    <h3>{{ subtitle }}</h3>

    <details v-for="{ question, answer, itemId } in subItems" :key="itemId">
      <summary>{{ question }}</summary>
      <div>{{ answer }}</div>
    </details>
  </section>

  <details v-for="{ question, answer, itemId } in items" :key="itemId">
    <summary>{{ question }}</summary>
    <div>{{ answer }}</div>
  </details>
</section>
```

**Good**

By not destructuring, the nested `v-for` loops are much easier to understand.

```vue
<section v-for="category in FAQs" :key="category.id">
  <h2>{{ category.title }}</h2>

  <section v-for="subcategory in category.subcategories" :key="subcategory.id">
    <h3>{{ subcategory.title }}</h3>

    <details v-for="item in subcategory.items" :key="item.id">
      <summary>{{ item.question }}</summary>
      <div>{{ item.answer }}</div>
    </details>
  </section>

  <details v-for="item in category.items" :key="item.id">
    <summary>{{ item.question }}</summary>
    <div>{{ item.answer }}</div>
  </details>
</section>
```

Note that while these examples with nested `v-for` loops are severe, they highlight a possible problem with destructuring in HTML templates. As a team, we decided to favor consistancy, and rather than have a rule like "always destructure except in loops," we've standardized on "avoid destructuring in templates."
