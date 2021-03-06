# Chai A11y aXe

[//]: # (AUTO INSERT HEADER PREPUBLISH)

This module provides a Chai plugin to perform automated accessibility tests via axe.

::: tip
This is part of the default [open-wc testing](https://open-wc.org/testing/) recommendation
:::

## Testing for Accessibility

### Chai BDD UI

The BDD UI works with chai's `expect` function.

Because the test is asynchronous, you must either await its result or pass a `done` parameter in the plugin's options object.

Rules can be ignored by passing `ignoredRules` with a list of ignored rules as a configuration option.

```js
import { fixture, expect, html } from '@open-wc/testing';

it('passes accessibility test', async () => {
  const el = await fixture(html`<button>label</button>`);
  await expect(el).to.be.accessible();
});

it('fails without label', async () => {
  const el = await fixture(html`<div aria-labelledby="test-x"></div>`);
  await expect(el).not.to.be.accessible();
});

it('passes for all rules, ignores attributes test', async () => {
  const el = await fixture(html`<div aria-labelledby="test-x"></div>`);
  await expect(el).to.be.accessible({
    ignoredRules: ['aria-valid-attr-value']
  });
});

it('accepts "done" option', (done) => {
  fixture(html`<button>some light dom</button>`)
  .then((el) => {
    expect(el).to.be.accessible({
      done
    });
  });
});
```

### Chai TDD UI

The `isAccessible()` and `isNotAccessible()` methods work on Chai's `assert` function.

```js
import { fixture, assert, html } from '@open-wc/testing';

it('passes axe accessible tests', async () => {
  const el = await fixture(html`<button>some light dom</button>`);
  await assert.isAccessible(el);
});

it('accepts ignored rules list', async () => {
  const el = await fixture(html`<div aria-labelledby="test-x"></div>`);
  await assert.isAccessible(el, {
    ignoredRules: ['aria-valid-attr-value']
  });
});

it('passes for negation', async () => {
  const el = await fixture(html`<div aria-labelledby="test-x"></div>`);
  await assert.isNotAccessible(el);
});
```

<script>
  export default {
    mounted() {
      const editLink = document.querySelector('.edit-link a');
      if (editLink) {
        const url = editLink.href;
        editLink.href = url.substr(0, url.indexOf('/master/')) + '/master/packages/chai-a11y-axe/README.md';
      }
    }
  }
</script>
