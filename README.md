# jest-issue-11802
https://github.com/facebook/jest/pull/11802

### Steps to reproduce the bug

```
$ git clone git@github.com:antongolub/jest-issue-11802.git
$ yarn
$ nvm use 16
Now using node v16.7.0 (npm v7.21.0)
$ node src/main/js/index.js
globbySync [Function: globbySync] # code is runnable
```

**success**
```
jest-issue-11802 % NODE_OPTIONS=--experimental-vm-modules npx jest
(node:68620) ExperimentalWarning: VM Modules is an experimental feature. This feature could change at any time
(Use `node --trace-warnings ...` to show where the warning was created)
 PASS src/test/js/index.js
    ✓  (2 ms)

----------|---------|----------|---------|---------|-------------------
File      | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s 
----------|---------|----------|---------|---------|-------------------
All files |       0 |        0 |       0 |       0 |                   
 index.js |       0 |        0 |       0 |       0 |                   
----------|---------|----------|---------|---------|-------------------
Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total

```



**failure**
```
$ nvm use 14
Now using node v14.17.1 (npm v6.14.13)
node src/main/js/index.js
globbySync [Function: globbySync] # code is runnable
```
```
jest-issue-11802 % NODE_OPTIONS=--experimental-vm-modules npx jest
(node:68864) ExperimentalWarning: VM Modules is an experimental feature. This feature could change at any time
(Use `node --trace-warnings ...` to show where the warning was created)
 FAIL  src/test/js/index.js
  ● Test suite failed to run

    Cannot find module 'node:fs' from 'node_modules/globby/index.js'

      at Resolver.resolveModule (node_modules/jest-resolve/build/resolver.js:313:11)
          at async Promise.all (index 0)

----------|---------|----------|---------|---------|-------------------
File      | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s 
----------|---------|----------|---------|---------|-------------------
All files |       0 |        0 |       0 |       0 |                   
 index.js |       0 |        0 |       0 |       0 |                   
----------|---------|----------|---------|---------|-------------------
Test Suites: 1 failed, 1 total
Tests:       0 total
Snapshots:   0 total
```