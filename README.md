# Restaurant Tech Stack Analyzer

An intelligent scraping agent that identifies a restaurant's Point of Sale (POS), Website Builder, and Event Management software. It uses a multi-step AI workflow to navigate websites like a human to find the "source of truth" for tech usage. It is currently a Python Notebook.

## How It Works

1.  **Initial Crawl (`Crawl4AI`):** Scrapes the homepage for scripts, footer text, and all links.
2.  **Link Classification (`Gemini 2.5 Flash`):** Intelligently categorizes links into `Ordering`, `Gift Cards`, `Private Events`, or `Instagram` based on context, not just keywords.
3.  **Deep Dive Navigation:**
    *   Iterates through **Ordering** and **Gift Card** links.
    *   **Follows Redirects:** Detects if `/order` redirects to `toasttab.com`.
    *   **Scrapes Sub-pages:** Finds external POS buttons embedded on internal ordering pages.
4.  **Tech Analysis (`Gemini 3 Pro`):** Aggregates deep-dive signals, scripts, and footer data to reason out the specific POS (e.g., Toast, SpotOn) and CMS (e.g., BentoBox).
5.  **Event Check:** specifically hunts for Tripleseat integration on private event pages.

## Tech Stack

*   **Python 3.13+**
*   **Crawl4AI:** For high-performance, async web scraping.
*   **BeautifulSoup4:** For HTML parsing and script extraction.
*   **Google GenAI SDK:**
    *   *Gemini 2.5 Flash:* For high-speed link classification.
    *   *Gemini 3 Pro:* For complex reasoning and final stack determination.
*   **Pydantic:** For structured data validation.

## Installation

```bash
pip install requirements.txt
```

## Configuration

Set your Google API key as an environment variable:

```bash
export GOOGLE_API_KEY="your_api_key_here"
```