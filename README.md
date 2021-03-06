# three-js-csg-es6
forked from https://github.com/james-oldfield/three-js-csg
**three-js-csg-es6** is a wrapper for NPM around [chandlerprall's](https://github.com/chandlerprall/ThreeCSG) Constructive Solid Geometry port to three.js. This package provides support for use with ES2015/AMD/CommonJS style modularity and composability.

## install

`npm i --save three-js-csg-es6`

## example mesh module

```js
 
import { ThreeBSP } from 'three-js-csg-es6'
import { BoxGeometry, Mesh, MeshPhongMaterial, SphereGeometry } from 'three'

export const meshFactory = () => {
  const box = new Mesh(new BoxGeometry(500, 100, 100));
  const sphere = new Mesh(new SphereGeometry(100, 50, 50));

  const sBSP = new ThreeBSP(sphere);
  const bBSP = new ThreeBSP(box);

  const sub = bBSP.subtract(sBSP);
  const newMesh = sub.toMesh();

  newMesh.material = new MeshPhongMaterial({ color: 0xdddddd, specular: 0x1a1a1a, shininess: 30, shading: THREE.FlatShading  });

  return Object.assign({}, { csg: newMesh  });

};
```
When instantiating the NPM module, it takes an instance of three.js therefore doesn't need to sit globally on the window object. In a currying-esque manner, the NPM module returns a function with which you can pass in three.js geometry like usual.

## demo

![three-js-csg-es6](./demo.png)

See a full demo using this module in this repo at: `./demo`. First clone the repo, run `npm install` and then `npm run watch`. Open `./demo/index.html` in browser to see the demo in action.
