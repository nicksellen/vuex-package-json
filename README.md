# reproduces issue with vuex not exporting package.json

(at least with my version of node, I think it's dependent on that, I have v17.9.0)

```
# install deps
yarn

# view quasar info
npx quasar info
```

It'll show a bunch of stuff including:

```
vuex - Not installed
```

... even when it is.

Quasar tries to load the package.json for vuex, but encounters this error (not printed out by default, I manually edited the quasar lib that does the loading to print the error)

```
Package subpath './package.json' is not defined by "exports" in /tmp/foo/quasar-project/node_modules/vuex/package.json
```

If I incorporate unreleased changes from #main branch, it works again! `npx quasar info` shows:

```
vuex - 4.0.2 -- state management for Vue.js
```

So, just needs a release!

The commit that fixes that is this one https://github.com/vuejs/vuex/commit/397e9fba45c8b4ec0c4a33d2578e34829bd348d7
