# Rick & Morty TV

```shell script
for f in *.jpg; do                           
  convert $f -resize 400 -quality 100% "${f%.jpg}-min.jpg"
done
```