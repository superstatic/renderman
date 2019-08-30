# Superstatic RenderMan

Superstatic RenderMan is a fast html, css, js renderer, using a puppeteer backend. RenderMan's main purpose is to render web content. The rendered content may be a static site, a React app etc. In that fashion RenderMan can be used as a static site generator, for server side rendering or for visual regression testing aswell. Through an elegant api RenderMan is a flexible renderer for the web.

## Architecture

RenderMan uses puppeteer as a headless Chrome backend. It's core represents an abstaraction to puppeteer and it's engine fires up a browser context. Core communicates in a reactive way with the engine and by using a high availability and fast render queue renders content in an instant. The rendered content can be manipulated by actions. Actions provide a simple api to manipulate the DOM, capture screenshots, pdfs etc. RenderMan is used by Superstatic to generate static sites. By utilising RenderMan's flexible architecture and api, rendering web content is fast and easy and things such as visual regression diff testing are possible, combined with Superstatic's powerful timeline feature.

RenderMan is asychronous by nature in a way that doesn't obstruct the developers workflow. Rendering can be done in stages and due to render queue's intelligent caching and a diff algorithm RenderMan renders only the content that has changed, making it a fast and powerful tool.

## Quality Assurance

Since RenderMan runs on top of a puppeteer backend rendering web content comes with automated form submission, UI testing, keyboard input, etc. Also, capturing timeline traces helps diagnose performance issues.

## Usage

```js
const renderman = new RenderMan(); // create an instance of RenderMan

(async () => {
  const markup = `<html><body>Hello, RenderMan!</body></html>`;

  const browser = await renderman.launch();
  await browser.render(markup);
  // do some stuff or render some more content!

  const document = await browser.document(); // capture the document
  document.body.innerHTML = `⚡️`;
  await browser.update() // update only the things that have changed

  await browser.destroy() // gracefully stop RenderMan
});
```