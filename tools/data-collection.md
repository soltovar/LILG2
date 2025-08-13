# Data collection
In order to scrape the links to all the public TikTok videos on the target profile, I ran a series of JavaScript scripts on my browser using developer mode. Said scripts can be found on [Responsive Muse](https://responsive-muse.com/export-tiktok-channel-video-titles-urls-using-javascript/) and there is a handy video tutorial there as well. I will reproduce the scripts below.\
\
This one **scrolls to the bottom of the page**:
```
let goToBottom = setInterval(() => window.scrollBy(0, 400), 1000);
```

This one **extracts the video titles and URLs and display them in the console**:
```
    clearInterval(goToBottom);
    let arrayVideos = [];
    console.log('\n'.repeat(50));
    const containers = document.querySelectorAll('[class*="-DivItemContainerV2"]');  
    for (const container of containers) {
        const link = container.querySelector('[data-e2e="user-post-item"] a');
        const title = container.querySelector('[data-e2e="user-post-item-desc"] a');
        //If the link is https://www.tiktok.com/, set it as the current page URL
        if (link.href === 'https://www.tiktok.com/') link.href = window.location.href;
        arrayVideos.push(title.title + ';' + link.href);
        console.log(title.title + '\t' + link.href);
    }
```

And the last one **exports the data as a .csv file** (with a semicolon as a separator!)
```
    let data = arrayVideos.join('\n');
    let blob = new Blob([data], {type: 'text/csv'});
    let elem = window.document.createElement('a');
    elem.href = window.URL.createObjectURL(blob);
    elem.download = 'my_data.csv';
    document.body.appendChild(elem);
    elem.click();
    document.body.removeChild(elem);
```
I imported the .csv file into Google Sheets and used the function `=IMPORTXML(URL, xpath_query)` to get the caption or text that appears below the videos on TikTok (I replaced `URL` with a reference to the cell that had my URL, e.g. `A1`, and selected `"//title"` as my `xpath_query`). 
</br></br>
As a result, I obtained the text that I used to look for videos that may be relevant (i.e. videos including the terms <i>pronoun</i> or <i>neopronoun</i>, or a construction in the format [neopronoun]/[neopronoun]). To do that, I used the function `=IF(ISNUMBER(SEARCH(search_for, text_to_search)), "Yes", "No")`, which allowed me to search for said instances in the retrieved text and to filter out videos that did not include any of those keywords.
</br></br>
Once I filtered the videos, I downloaded them using [JDownloader 2](https://jdownloader.org/), simply copying the list of URLs and pasting them into the LinkGrabber. For this to work, it is crucial to have the TikTok plugin activated in the settings.
