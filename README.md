# WebScraping
Web Scraping Fake Job Listings from  a fake Job Posting Website

### Web Scraping Fake Job Listings from Real Python

This Python script is designed to scrape job listings from the Real Python fake job listings website. It retrieves the job titles, companies, locations, and "Apply" links for Python-related jobs.

#### How it Works

1. **Sending HTTP Request and Parsing HTML**

   The script sends a GET request to the Real Python fake job listings URL using the `requests.get()` function from the `requests` module. It then parses the HTML content of the page using BeautifulSoup from the `bs4` library.

   ```python
   import requests
   from bs4 import BeautifulSoup

   url = "https://realpython.github.io/fake-jobs/"
   page = requests.get(url)
   soup = BeautifulSoup(page.content, "html.parser")
   ```

2. **Finding Job Listings**

   It searches for the container of job listings by finding an element with the ID "ResultsContainer".

   ```python
   results = soup.find(id="ResultsContainer")
   ```

3. **Filtering Python Jobs**

   The script filters job listings to only those containing the word "python" in their titles. It finds all `<h2>` elements with the specified condition.

   ```python
   python_jobs = results.find_all("h2", string=lambda text: "python" in text.lower())
   ```

4. **Extracting Job Details**

   Initially, the script attempted to extract job details directly from the filtered `<h2>` elements. However, it found that these elements did not include complete job information, resulting in errors.

   ```python
   '''
   # Extracting job details directly from <h2> elements
   for jobP in python_jobs:
       job_title = jobP.find("h2", class_="title is-5")
       company = jobP.find("h3", class_="subtitle is-6 company")
       location = jobP.find("p", class_="location")
       print(job_title.text.strip())
       print(company.text.strip())
       print(location.text.strip())
       print()
   '''
   ```

   Another attempt was made to extract job details from all job listings. This time, it looped over all job elements and extracted details such as title, company, and location.

   ```python
   '''
   # Extracting job details from all job listings
   for job_element in job_elements:
       job_title = job_element.find("h2", class_="title is-5")
       company = job_element.find("h3", class_="subtitle is-6 company")
       location = job_element.find("p", class_="location")
       print(job_title.text.strip())
       print(company.text.strip())
       print(location.text.strip())
       print()
   '''
   ```

5. **Extracting "Apply" Links**

   The final approach was to extract "Apply" links for each Python job listing. It iterates over the parent elements of the filtered `<h2>` elements and finds all `<a>` elements within them.

   ```python
   for job_element in python_job_elements:
       links = job_element.find_all("a")
       for link in links:
           link_url = link["href"]
           print(f"Apply here: {link_url}\n")
   ```

   This successfully extracts the URLs for applying to Python job listings.


This README file provides an overview of the script's functionality and explains each part of the code, including the commented-out sections.
