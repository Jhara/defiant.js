[![](http://goo.gl/z6qgCa)](http://defiantjs.com/)

DefiantJS provides the ability for you to build smart templates applicable on JSON structures, based upon proven &amp; standardized technologies such as XSLT and XPath.

DefiantJS also extends the global object __JSON__ with the method "__search__", which enables searches on JSON structures with XPath expressions and returns matches as an array-like object.

For detailed information, please visit [defiantjs.com](http://defiantjs.com) and try out the [XPath Evaluator](http://www.defiantjs.com/#xpath_evaluator).

###Update v1.2.0
As of version 1.2.0, the __snapshot__ feature was added. Using this feature, the performance of the search is increased by more than 100 times. Use 'snapshot search' when you are certain that the JSON structure hasn't been changed. If the structure changes, create a new snapshot and always make searches on the latest snapshot. The example below shows how it can be used.

###Example usage
* Snapshot feature
```js
var data {
	// ...large JSON structure...
};

// Regular search
found = JSON.search(data, '//item');

var snapshot = Defiant.getSnapshot(data);
// Snapshot search - this is more than 100 times faster than 'regular search'
found = JSON.search(snapshot, '//item');
```

* Simple search
```js
var data = [
       { "x": 2, "y": 0 },
       { "x": 3, "y": 1 },
       { "x": 4, "y": 1 },
       { "x": 2, "y": 1 }
    ],
    res = JSON.search( data, '//*[ y > 0 ]' );

console.log( res );
// [{ x=3, y=1}, { x=4, y=1}, { x=2, y=1}]
```

* XSLT Templating
```html
<!-- Defiant template -->
<script type="defiant/xsl-template">
    <xsl:template name="books_template">
        <xsl:for-each select="//movie">
            <xsl:value-of select="title"/><br/>
        </xsl:for-each>
    </xsl:template>
</script>
 
<script type="text/javascript">
    var data = {
            "movie": [{"title": "The Usual Suspects"},
                      {"title": "Pulp Fiction"},
                      {"title": "Independence Day"}]
        },
        htm = Defiant.render('books_template', data);
    console.log(htm);
    // The Usual Suspects<br>Pulp Fiction<br>Independence Day<br>
</script>
```

// Changelog
`1.2.2` The XPath method 'contains' is automatically case insensitive 
`1.2.0` Added snapshot search feature
