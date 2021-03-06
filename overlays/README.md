# bpmn-js overlays example

This example shows how to use the overlays api of [bpmn-js](https://github.com/bpmn-io/bpmn-js) to attach HTML overlays to a BPMN 2.0 diagram.


## About

The example loads a process diagram on how to process QR codes and attaches a note on it using the `overlays` service.

![QR-CODE workflow process](./docs/qr-code.png "Screenshot of the example process.")


## Usage summary

Access the `overlays` service via `bpmnViewer.get('overlays')` and add overlays to elements by id using the `Overlays#add` method.

```javascript
var overlays = bpmnViewer.get('overlays');

// attach an overlay to a node
overlays.add('SCAN_OK', {
  position: {
    bottom: 0,
    right: 0
  },
  html: '<div>Mixed up the labels?</div>'
});
```

The method `Overlays#add` receives two important parameters:

* a element or elementId
* a overlay descriptor

The overlay descriptor must contain a `html` element you want to attach as the overlay as well as a `position` that indicates where you want the overlay to be added on the element. Use `top`, `left`, `bottom`, `right` to control the attachment.


## Setting up bpmn-js

You need to get hold on the bpmn-js first. Get it via [bower](https://github.com/bpmn-io/bpmn-js-examples/tree/master/simple-bower) or [npm](https://github.com/bpmn-io/bpmn-js-examples/tree/master/simple-commonjs).

To use `overlays` and other services provided by bpmn-js instantiate bpmn-js (this time the viewer) via

```javascript
var bpmnViewer = new BpmnViewer({
  container: '#canvas',
  width: '100%',
  height: '100%'
});
```

Import a BPMN 2.0 diagram and add the overlays in the `done` callback:

```javascript
bpmnViewer.importXML(diagramXML, function(err) {

  if (err) {
    return console.error('could not import BPMN 2.0 diagram', err);
  }

  // retrieve services and work with them
  bpmnViewer.get('overlays').add(...);
});
```


## Building the Project

Initialize the project dependencies via

```
npm install
```

The project contains a  [Grunt](http://gruntjs.com/) build script that defines a few tasks.

To create the sample distribution in the `dist` folder run

```
grunt
```

To bootstrap a development setup that spawns a small webserver and rebuilds your app on changes run

```
grunt auto-build
```


## License

MIT
