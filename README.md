# vuejs-icons-font-map
A simple vuejs filter that would map fontawesome icon names to hex characters to use in templates.

run this command to make the dictionary:
```
perl -n -e'/\.([\w-]+):before|content(:) "\\([\w\d]{4})"; }(\n)/ && print "$2\"$1$3\"$4"' fontawesome-free-5.9.0-web/css/all.css | sed -e 's/$/,/' > icon-dict.js
```
then add `export default {` as the first line of the `icon-dict.js` file and add `}` as the last line.
put the file in your app(in case of nativescript-vue) or src(in case of plain vue) directory next to the `main.js` file.

And add this to your main.js before you initialize Vue(`new Vue`).
```
import icon_map from "./icon-dict";
Vue.filter("iconmap", (value) => {
  return String.fromCharCode(parseInt(icon_map[value], 16));
});
```
Then you can do something like this in your templates:

**nativescript:**
```
<label class="fas">{{"fa-info-circle" | iconmap}}</label>
```

**html**
```html
<span class="fas">{{info | iconmap}}</span>
```

While having this in your global css file:
```css
.far {
  font-family: "fa-regular-400";
}

.fab {
  font-family: "Font Awesome 5 Brands", "fa-brands-400";
}

.fas {
  font-family: "Font Awesome 5 Free", "fa-solid-900";
}
```

You also need to put the .ttf files of your fonts in a directory calles fonts next to
the `main.js` file or `assents` directory of your project. In my case I have these
fonts there:
> fa-regular-400.ttf  fa-solid-900.ttf  IcoMoon-Free.ttf

### IconMoon:
run
```
perl -n -e'/\.([\w-]+):before|content(:) "\\([\w\d]{4})";(\n)/ && print "$2\"$1$3\"$4"' IcoMoon-Free-master/Font/demo-files/demo.css | sed -e 's/$/,/' | head -n -1 > icon-dict.js
```
Remove `"clearfix"` from the beginning of the file. then insert all the lines in the file at the end of the dictionary file you had created for fontawesome. 
Add put the .ttf file next to the fontawesome .ttf files and add this to your css:
```css
.ico {
  font-family: "IcoMoon-Free";
}
```
Now you can do this in your templates:
```
<label class="ico">{{"icon-info" | iconmap}}</label>
```

PS. my perl is bad. And my regex is pretty cryptic because I'm not so experienced with perl.
feel free to make it better.
I made this repo because I had to struggle sooooo much to work with fonticon and friends and nothing worked for me.
