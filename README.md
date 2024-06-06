# Bookmarklets For SEO: Potentially Useful Bits of Javascript

Below is a list of of bookmarklets that might be useful for SEO purposes...

For more of my SEO work, visit [https://rkseo.xyz](https://rkseo.xyz)

## What Is A Bookmarklet? And how to use this...
A bookmarklet is just a bit of javascript code that you can store as a bookmark in your browser. Whenever you click the bookmark, it executes the javascript code. 

All you need to do is copy and paste the below blocks of code (including "javascript:") into a bookmark url and name it appropriately. 

Clicking it executes the code, and does what the description says. 

### Bookmarklets for SEO:

Reformat a list of keywords from separate lines, to single line with commas. 
```
javascript: 
(function() {
    var input = prompt('Enter keywords, each on a new line:');
    if (input) {
        var keywords = input.split('\n').map(function(keyword) {
            return keyword.trim();
        });
        alert(keywords.join(', '));
    }
})();
```

Semrush Exact: SEO overview of exact page in new tab

```
javascript:
(function() {
    const currentPageUrl = encodeURIComponent(window.location.href);
    const semrushUrl = `https://www.semrush.com/analytics/organic/overview?db=us&q=${currentPageUrl}&searchType=url`;
    window.open(semrushUrl, '_blank');
})();
```



Semrush Root: SEO info on root domain
```
javascript:
(function() {
    const currentPageUrl = encodeURIComponent(window.location.href);
    const semrushUrl = `https://www.semrush.com/analytics/organic/overview?db=us&q=${currentPageUrl}&searchType=domain`;
    window.open(semrushUrl, '_blank');
})();
```

Headings: Copies h-tags on the current page to clipboard.
```
javascript:
(function() {
    let hTags = ['h1', 'h2', 'h3', 'h4', 'h5', 'h6'];
    let hTexts = [];
    hTags.forEach(tag => {
        let elements = document.querySelectorAll(tag);
        elements.forEach(element => {
            hTexts.push(tag.toUpperCase() + ": " + element.innerText);
        });
    });
    let textToCopy = hTexts.join('\n');
    let tempElem = document.createElement('textarea');
    tempElem.value = textToCopy;
    document.body.appendChild(tempElem);
    tempElem.select();
    document.execCommand('copy');
    document.body.removeChild(tempElem);
    alert('H-tags copied to clipboard!');
})();
```

Keyword: Enter a specific keyword. Get the following info from the current page: 
- Word / Phrase Count
- Keyword Density
- Total Word Count
- Total Headings
- Total Images
```
javascript:
(function() {
    var titles = [];
    var results = document.querySelectorAll('h3');
    for (var i = 0; i < Math.min(10, results.length); i++) {
        titles.push(results[i].textContent);
    }
    var textToCopy = titles.join('\n');
    var textArea = document.createElement('textarea');
    textArea.value = textToCopy;
    document.body.appendChild(textArea);
    textArea.select();
    document.execCommand('copy');
    document.body.removeChild(textArea);
    alert('Top 10 Google search results copied to clipboard!');
})();
```

Multi-Keyword: Same information as keyword, across multiple terms. 
```
javascript:
(function() {
    function countPhrase(text, phrase) {
        const regex = new RegExp('\\b' + phrase.trim().replace(/[-/\\^$*+?.()|[\]{}]/g, '\\$&') + '\\b', 'gi');
        return (text.match(regex) || []).length;
    }

    function keywordDensity(phraseCount, totalWordCount) {
        return ((phraseCount / totalWordCount) * 100).toFixed(2);
    }

    function copyToClipboard(text) {
        const textarea = document.createElement('textarea');
        textarea.textContent = text;
        document.body.append(textarea);
        textarea.select();
        document.execCommand('copy');
        textarea.remove();
    }

    const phrasesInput = prompt('Enter words or phrases to search separated by commas:');
    if (phrasesInput) {
        const textContent = document.body.innerText;
        const totalWordCount = textContent.match(/\b\w+\b/g).length;
        const headingsCount = document.querySelectorAll('h1, h2, h3, h4, h5, h6').length;
        const imagesCount = document.querySelectorAll('img').length;
        const phrases = phrasesInput.split(',');
        let results = [];

        for (let phrase of phrases) {
            const phraseCount = countPhrase(textContent, phrase);
            const density = keywordDensity(phraseCount, totalWordCount);
            results.push(`Word/Phrase: ${phrase.trim()}\nCount: ${phraseCount}\nKeyword Density: ${density}%`);
        }

        const result = `${results.join('\n\n')}\n\nTotal Word Count: ${totalWordCount}\nTotal Headings: ${headingsCount}\nTotal Images: ${imagesCount}`;
        copyToClipboard(result.trim());
        alert(result.trim() + '\n\nThis information has also been copied to your clipboard.');
    }
})();
```

GSC Page: Opens the current page in your GSC view. replace "DOMAIN.com" with your gsc domain (ex: ...domain%3google.com&page...)
```
javascript:
(function() {
    const currentPageUrl = encodeURIComponent(window.location.href);
    const gscURL = `https://search.google.com/search-console/performance/search-analytics?resource_id=sc-domain%3ADOMAIN.com&page=*${currentPageUrl}&searchType=url`;
    window.open(gscURL, '_blank');
})();

```
