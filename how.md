You can use `wget` with several flags to ensure not only the HTML file but also all the dependent assets (images, CSS, JavaScript, etc.) get downloaded. A commonly used command for this is:

```bash
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent https://avada.website/spa/
```

Here’s what each flag does:

- **`--mirror`**  
  Activates options suitable for mirroring: recursive download, time-stamping, and more.
  
- **`--convert-links`**  
  Converts the links in the downloaded documents to point to the local files so that the website remains navigable offline.
  
- **`--adjust-extension`**  
  Ensures that files are saved with the correct extensions (for instance, adding `.html` to files that need it).
  
- **`--page-requisites`**  
  Downloads all the resources (images, stylesheets, scripts) that are required to display the page correctly.
  
- **`--no-parent`**  
  Prevents downloading files from parent directories, keeping the scope limited to the specified URL.

**Note:**  
Since the URL you provided (https://avada.website/spa/) points to a single-page application (SPA), the content might be assembled dynamically via JavaScript. In such cases, `wget` will only retrieve the initial HTML and the statically referenced objects. If essential content loads dynamically (after the initial page load), you might want to consider alternative tools such as **HTTrack** or use a headless browser (like **Puppeteer** or **Selenium**) to capture the fully rendered page.

For instance, with **HTTrack**, you can run:

```bash
httrack https://avada.website/spa/ -O ./local-folder "+*.avada.website/*" -v
```

This will mirror the site and download resources while following internal links.  

Both approaches have their strengths—`wget` is great for mostly static sites, while headless browsing or HTTrack may better handle dynamic SPAs. Choose according to your needs.

Beyond this straightforward download process, you may explore tools like **Puppeteer** for more advanced use cases. Puppeteer lets you script a headless Chrome session, so you can wait for all dynamic content to load before saving the full rendered HTML. This is particularly useful if your webpage relies heavily on JavaScript. If you're interested, I could share a sample Puppeteer script to capture the rendered page for offline viewing.
