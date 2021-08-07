# Comments

### Write the least possible comments

* Prefer coding to commenting
* The code should document itself as most as possible
* Many and long comments are code smell

### Comments Should Be

* Meaningful
* Necessary
* Readable

### Bad Comments

* „Commented out” code - _Remove it, find it in the version control system_
* Separators, markers
* Redundant
* Misleading
* Out-of-date
* Obvious
* Unnecessary
* Funny
* Closing brace comment
* Attributes - _author, date, issue number, etc._
* Non-English
* Too many HTML markers
* Historical
* Prone to copy-paste error

### Good Comments

* TODO comments
* Warnings - _e.g. "Not threadsafe"_
* Limitations - _e.g. "It works only with a sorted list"_
* Javadoc comment to public API - _for high level service methods_
* Comment empty blocks
* Less is more.

Example: Bad: Comments

```java
// Redundant, obvious:
/**
* gets the value of Name
*/
public String getName();

// Funny, unnecessary:
// I invented this part, but do not know why
```

Example: Good: Javadoc comment

```java
/**
* Returns an Image object that can then be painted on the screen.
* The url argument must specify an absolute {@link URL}. The name
* argument is a specifier that is relative to the url argument.
* <p>
* This method always returns immediately, whether or not the
* image exists. When this applet attempts to draw the image on
* the screen, the data will be loaded. The graphics primitives
* that draw the image will incrementally paint on the screen.
*
* @param url an absolute URL giving the base location of the image
* @param name the location of the image, relative to the url argument
* @return the image at the specified URL
* @see Image
*
* @deprecated Use {@link getImage(Long id)} instead.
*/
@Deprecated
public Image getImage(URL url, String name) {
    try {
        return getImage(new URL(url, name));
    } catch (MalformedURLException e) {
        return null;
    }
}
```



