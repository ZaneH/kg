---
title: Frontend Web Development
tags: web, frontend, code
---

## The Rundown

Prominent tools such as Vite, Svelte, Solid, Next.js, and React remain popular for diverse projects, though the field's dynamic nature demands an openness to adapting.

The most important thing to understand when starting off is reactivity. Reactivity is the idea that when data (or "state") changes, the UI updates to reflect that change. This is the core of modern frontend web development. Then you can apply your HTML & CSS knowledge and boom, you're a frontend web developer.

By blending coding with design, frontend development offers a creative space to craft seamless user experiences. Notably, React continues to offer extensive job opportunities and has a lively ecosystem.

>[!note]
>
>There are also tools like Phoenix or Ruby on Rails that provide the tools necessary for full-stack web development. They often use a templating engine that combine [[code/overview/backend-web-development|backend]] data with frontend "views."

>[!tip]
>
>I typically reach for **React** when I'm building a "web app" and **Next.js** when I'm building a "website."
>
>The difference is that web apps are typically more interactive and require a lot of local state management. Websites are typically more static and don't require much state management. Next.js has the added benefit of code splitting automatically and allowing for server-side rendering, which can be powerful for SEO rankings and performance.

### Requirements

Here are some of the specific tools frontend web devs use frequently:

- **Code Editors (e.g., VSCode):** Use efficient code editors for coding convenience.
- **JavaScript** - JavaScript is inescapable as a frontend web developer. Best to learn it.
- **HTML & CSS**
	- Adding styles, flex layouts, media queries, etc.
	- Tools like Tailwind allow you to "skip" learning CSS.
- **Command Line** - Familiarity `bash`, `git`, `npm`/`yarn` and `node` will go a long way.
    - There are an endless amount of tools that can be learned here.
- **Web Hosting** - Putting your website up on the Internet is an important skill. I always recommend Vercel. You can even attach custom domains and host all your sites for free.
- **Browser developer tools**
	- Being able to inspect element and understand exactly what's going on is vital. From CSS styles to network requests, the browser developer tools offer a lot.
- **Figma** - Vital for communicating designs.
- **APIs** - Being able to fetch data from an API is crucial. I recommend learning `fetch` for Next.js and `wretch` for React. How you handle the API data often depends on if your app is server-side rendered or not.

## Web Design

By using the tools available, the browser can render just about anything. A big part of frontend web development is implementing the [[code/overview/web-design|web design]] that comes from a web designer if you're lucky.

Web designs are typically made in Figma nowadays but they may come in a variety of formats, including napkin sketches.

Many developers I've spoken to have expressed that design is difficult. I can relate, and there are a few tricks to make it easier.

- Dive into "Component Libraries"
	- You'll start to notice a common pattern of components (e.g. Cards, Breadcrumbs, Navbar) that are used to compose just about every modern website.
	- [My favorite component libraries](https://github.com/stars/ZaneH/lists/react-component-libraries)
- Use a Component Library
	- Odds are there's one available for your setup. Find one and just use it! No need to design anything now, just put things together.
	- There is such thing as a bad component library, but it's subjective.
- Learn Figma
	- There are a variety of tools that will change the way you think about layouts (Auto Layout) and design in general.
	- CSS code can be copied from the sidebar.
	- Being able to visualize a design before coding it can prevent wasted code.
	- There is a "Dev Mode" which helps developers implement the Figma design down to the last pixel.
- Practice
	- Copy designs from existing websites in Figma.
	- Design fake webpages or components.
	- Build a desktop, tablet, and mobile layout for a single page.
		- Figure out how to use Auto Layout to make your life easy.
	- Add animations to your designs.

## State

Typically, frontends are responsible for handling a certain amount of "state" or data. Like when you change a dropdown menu, it likely isn't updating anything on the server, instead that value is stored in the frontend as state for later use.

```javascript
...
onChange={(option) => {
	setSize(option); // local state update
}}
...
```

Managing state is an opinionated topic. Redux used to be the goto solution, but it appears more fractured now. To reduce dependencies in my projects, I typically use `useState` and `useContext` (provided by React) to manage state across my components.

>[!note]
>`useState` resets if you reload the page. There are again, a bunch of options to solve this. My current favorite is using something like Mantine's `useLocalStorage` hook which adds "persistent storage" to React's `useState`.

Managing state usually isn't too difficult, but it requires a bit of thought to do it well.

## Good to Know

These are not vital for frontend web development, but they are good to know about and can do cool things.

- **WebSockets (and/or socket.io):** Enable real-time communication between clients and servers, facilitating interactive features like chat applications and live updates.
- **SSR (Server Side Rendering):** This is a loaded term, but think of it like this: Instead of the browser making the network calls to populate the pages content, SSR renders the page on the server and gives it to the client. This provides quite a few benefits. Next.js is known for this.
- **LocalStorage:** Store key-value pairs in a user's browser for lightweight data persistence, useful for tasks like caching or storing user preferences.
- **WebAssembly:** Compile languages like C, C++, or Rust to run code in the browser at near-native speed, unlocking high-performance web applications.
- **CSS Preprocessors (e.g., Sass, Less):** Write cleaner and more efficient CSS using preprocessing languages that offer variables, mixins, and other advanced features.

## Interesting Repos

Here are few GitHub lists that contain projects I found interesting. They all relate to frontend programming:
- [React Components](https://github.com/stars/ZaneH/lists/react-components) - React components to drop into your project.
- [Web Frameworks](https://github.com/stars/ZaneH/lists/web-frameworks) - Build your next project using one of these?
- [Site Generators](https://github.com/stars/ZaneH/lists/site-generators) - The frontend is done for you. Just modify it.
- [React Component Libraries](https://github.com/stars/ZaneH/lists/react-component-libraries) - Full component libraries to use in your project.