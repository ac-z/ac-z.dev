![ARISE](./docs/logo/arise-logo_transparent.png)

# The Bash Static Site Generator
*A step back from [Ghost](https://ghost.org/), in the shell.*

---

## TODO
- Create new metadata types that are needed for better control:
    - `show_date` - Determine whether a date snippet is appended to the page or not
- Create GitHub actions script for deploying to GitHub Pages or other cloud location from a repo

### Documentation Tasks
- Scrub personal site details out and create a real template website that is better for showcasing the program
- Add a license file
    - Add licensing documentation for logo fonts. Both are CC-BY-SA so should be pretty simple, but I want to make a readme for attribution nonetheless
- Write a real readme to showcase this project


### Dependencies
- Bash 5.1
    - **Used for:** 😐
    - **Why:** Do you see what language this program is written in?
- [pandoc](https://pandoc.org/)
    - **Used for:** `build_page` - Function that builds pages from a `.md` source file
    - **Why:** Arise uses Pandoc for conversion of Markdown to HTML. If your source pages are already in HTML and you don't need Markdown conversion, you can disable Markdown conversion on individual pages with the use of an Arise page option (see above).
- GNU `date`
    - **Used for:** `build_rss` - RSS feed generator function
    - **Why:** You see, RSS is kind of ridiculous because it asks for dates in RFC-822 (stupid) rather than the usual ISO 8601 format used by developers who weren't dropped on their head as a child. GNU's implementation of the date command has a flag to accomodate this, but it's not available on BSD/macOS.
- GNU `find`
    - **Used for:** `build_toc` - Function that builds TOC/index pages
    - **Why:** Only the GNU version supports `-maxdepth`. This flag is used for the TOC indexer function to ensure that only folders in the current directory (and not subfolders of those) get put into your indices.
- GNU `awk`
    - **Used for:** `evaluate_inline` - Function that performs inline bash snippet evaluations. This is disabled by default because this functionality is still WIP.
    - **Why:** Using `awk` in any capacity is the equivalent of staring into a horrific eldrich abyss not meant for mere mortals. Making those commands portable is another story entirely.
- GNU `sed`
    - **Used for:** `build_header` - Function that populates headers with metadata from page source files
    Dependency for the header metadata tag population. 
    - **Why:** This script makes use of the GNU version of the '-i' flag. BSD sed will not let you run inline sed replacements without forcing you to do an extra file write to create a backup of the original file, which you then have to run ANOTHER command to delete (literally why).

### Roadmap / To-Do / Feature Ideas
- Refactor inline bash evaluation function and enable its usage. Right now it only works on very tiny/simple snippets because I wrote the logic for it because I thought it would be funny to implement (it was). I wasn't thinking of it in terms of a feature that is actually functional and practical to use, but I'd like to do that now.
   - Allow inline bash evaluations in the site headers and footers
- Add support for metadata tag usage in the site footer.
- Move the hardcoded TOC formatting in `build_toc` into a configurable template within `.config`
- Bundle and implement [Markdown.pl](https://daringfireball.net/projects/markdown/) as a fallback rendering engine for systems that do not have pandoc installed.
- Add support for inline include statements for html snippets saved in the `/config` folder so that it's possible to write reusable little bits for pages.
- Implement better error handling. Right now it's wishy washy and in many ways basically nonexistent-- most stuff will silently error or otherwise not gracefully cause an abort.
    - As far as dependency checks, right now it only checks if your bash version is good. Maybe could consider implementing checks for the other dependencies. It's really hard to determine if something is GNU or not, though.

### Legal & Acknowledgements
These can be found on a separate page [here](legal/README.md).
