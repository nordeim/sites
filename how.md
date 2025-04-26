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

---
This warning shows up because Git has a feature that normalizes line endings to ensure consistency across different operating systems. On Windows, Git’s default configuration (`core.autocrlf=true`) converts LF (Unix-style) line endings to CRLF (Windows-style) when you check files out, so that text editors on Windows work with the expected line endings. The warning message is Git telling you that while your files currently use LF, they will be converted to CRLF in your working copy when Git processes them.

To stop Git from changing LF to CRLF, you have a couple of options:

1. **Disable Automatic Conversion Globally**

   If you want Git to leave your line endings as they are (i.e., not perform any conversion), you can disable the automatic conversion by running:

   ```bash
   git config --global core.autocrlf false
   ```
   
   This setting tells Git not to convert line endings when checking out or committing files.

2. **Use the "input" Option (for Unix-style in the Repository)**
   
   If you'd like to keep LF in your repository while still allowing Git to convert CRLF to LF on commit (but not the other way around), set:
   
   ```bash
   git config --global core.autocrlf input
   ```
   
   With this setting, Git converts CRLF to LF on commit, but it leaves the working directory files unchanged.

3. **Specify Line Endings per File Type Using .gitattributes**
   
   You can enforce a specific line ending format by adding a `.gitattributes` file to your repository. For example, if you want all text files to always use LF, add:
   
   ```
   * text eol=lf
   ```
   
   This method ensures consistency regardless of individual Git configuration.

### Why Git Does This

Git’s line-ending normalization is designed to minimize issues when multiple developers work on different operating systems. Without normalization, you might see spurious changes in diffs or run into problems with scripts and tools expecting a particular line ending style. Essentially, Git is trying to enforce a consistent environment that reduces potential cross-platform issues.

Using any of the methods above will help you avoid the warning and maintain control over your file line endings. If you have more questions or need further details on configuring Git for cross-platform projects, let me know!

---
https://eternallybored.org/misc/wget/

Both approaches have their strengths—`wget` is great for mostly static sites, while headless browsing or HTTrack may better handle dynamic SPAs. Choose according to your needs.

Beyond this straightforward download process, you may explore tools like **Puppeteer** for more advanced use cases. Puppeteer lets you script a headless Chrome session, so you can wait for all dynamic content to load before saving the full rendered HTML. This is particularly useful if your webpage relies heavily on JavaScript. If you're interested, I could share a sample Puppeteer script to capture the rendered page for offline viewing.
