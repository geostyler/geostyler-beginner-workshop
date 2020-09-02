# geostyler-beginner-workshop
Workshop on how to use GeoStyler from scratch

The online workshop can be found on [https://geostyler.github.io/geostyler-beginner-workshop/](https://geostyler.github.io/geostyler-beginner-workshop/).

## Local Build

_The workshop requires you to have `jekyll` installed on your system. You can find detailed instructions on how to install it
on [https://jekyllrb.com/](https://jekyllrb.com/)._

Navigate into the `workshop/` directory and run

```bash
bundle exec jekyll build
```

to create a local build of the workshop, or

```bash
bundle exec jekyll serve
```

to also start a dev server that hosts the workshop on `localhost:4000`. Hot-reloading is activated by default.

## Run workshop application

You can run the final application by navigating into the `geostyler-app/` directory and running

```bash
npm i
npm start
```

The application is hosted on `localhost:3000`.

## <a name="license"></a>License

This workshop is released under the BSD 2-Clause license. Please see the file
[`LICENSE`](https://github.com/geostyler/geostyler-beginner-workshop/blob/master/LICENSE) in the
root of this repository.
