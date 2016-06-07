## grempe.github.io

This is a [Github pages](https://help.github.com/articles/using-jekyll-with-pages/) site and is served at [https://www.rempe.us](https://www.rempe.us). A cryptographically signed backup copy is running on the [Keybase File System (KBFS)](https://keybase.io/docs/kbfs) is at [https://grempe.keybase.pub/www.rempe.us/](https://grempe.keybase.pub/www.rempe.us/)

### Development

```
bundle install
bundle update
bundle exec jekyll serve --config _config.yml,_config_dev.yml --safe --watch --profile --incremental
```

### Deployment

#### Github

```
git push
```

#### Keybase

```
bundle exec jekyll build --config _config.yml,_config_keybase.yml -d /keybase/public/grempe/www.rempe.us --watch
```
