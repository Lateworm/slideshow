# Slideshow

A simple slideshow app for desktop and mobile. Built with Vue 3, TypeScript, and Font Awesome.

## Notes

### Direction

This project was set up with vue-cli, using the options for unit-testing and TypeScript. The advantages afforded here have not been fully realized yet:
- Unit testing should be a top priority if development continues.
- Typescript is largley ignored in the code as of now, any future work should improve TypeScript feature usage.

Dektop browser testing has been done in Chrome, Safari, and Firefox. Older browsers have not yet been tested.

### Known Issues

- Viewport height on mobile: Viewport height changes based on whether the navbar is visible. By using both default (static, for slides) and absolute (for interface overlays) positioning on this page, I exposed this problem in two different ways. It's an easy problem to miss because it does not occur in the mobile view of a desktop browser, but it's a well-known problem that I should have seen coming.
- Buttons on iOS: For some reason the left/right buttons render incorrectly in iOS.
- Accessibility: The buttons can be accessed and clicked via tab/enter, which shows the default accessibility outlines. Arrow key navigation currently does not add accessibilty feedback on-screen. I've used large buttons, but it would be prettier to reduce button size visually but add a larger hit target. Accessibility concerns here may be different than they are for more traditional docuemnt-like web content. I'm not sure what would be the proper use of semantic elements here.
- Loading: I've added loading indicators and disables navigation during loading, so things should be predictable. This is 'good enough', but I'm interested in the idea of 'double buffering' by loading images that may be navigated to next (one on either side), but this will take a little more time commitment.

## Usage

### Set up
```
npm install
```

### Serve with hot-reload for development
```
npm run serve
```

### Build for production
```
npm run lint
npm run build
```

### Test
```
npm run test:unit
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
