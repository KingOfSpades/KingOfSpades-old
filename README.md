This branch is for testing new things local, use the following command to run the site using a docker container:
```bash
$ docker run --rm -it --volume="$PWD:/srv/jekyll" --volume="$PWD/vendor/bundle:/usr/local/bundle" --env JEKYLL_ENV=development -p 4000:4000 jekyll/jekyll jekyll serve 
```
